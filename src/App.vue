<script setup>
import { ref, onMounted } from "vue";
import AdvantageCard from "./components/AdvantageCard.vue";
import SearchForm from "./components/SearchForm.vue";

const searchQuery = ref ('star-wars')
const cards = ref([]);

const loadData = async () => {
	if (!searchQuery.value) return

  try {
    const response = await fetch(
      `http://www.omdbapi.com/?apikey=a181cfa6&s=${searchQuery.value}`,
    );
    const data = await response.json();
    cards.value = data.Search || [];
  } catch (err) {
    console.error(err);
  }
};
onMounted(loadData)
</script>

<template>
  <div class="wrapper">
    <h1>Search the movie...</h1>

		<SearchForm
			v-model="searchQuery"
			@search="loadData"
		/>

    <div class="advantages-grid">
      <AdvantageCard v-for="card in cards" :key="card.imdbID" :item="card" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "./assets/mixins" as *;
.wrapper {
  padding-inline: toRem(15);
  padding-block: toRem(15);
  h1 {
    font-size: toRem(30);
		width: toRem(400);
		margin: 0 auto;
		margin-bottom: toRem(40);
  }
  .advantages-grid {
		padding: toRem(20);
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: toRem(20);
  }
}
</style>
