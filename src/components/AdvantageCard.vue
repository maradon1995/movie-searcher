<script setup>
defineProps({
  item: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <a 
    :href="`https://www.imdb.com/title/${item.imdbID}/`" 
    target="_blank" 
    class="card"
  >
    <div class="card__image">
      <img :src="item.Poster" :alt="item.Title" v-if="item.Poster !== 'N/A'">
      <div v-else class="card__no-image">No Poster</div>
    </div>
    
    <div class="card__content">
      <h3>{{ item.Title }}</h3>
      <p>{{ item.Year }}</p>
    </div>
  </a>
</template>

<style lang="scss" scoped>
@use "../assets/mixins" as *;

.card {
  display: flex;
	flex-direction: column;
	justify-content: space-between;
	align-items: center;
  text-decoration: none;
  color: inherit;
  
  padding: toRem(24);
  border: 1px solid #000;
  border-radius: toRem(12);
  @include adaptiveValue("width", 200, 100);
  
  transition: transform 0.3s ease, box-shadow 0.3s ease, scale 0.3s ease;

  &:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0,0,0,0.1);
		scale: 1.05;
  }

  .card__image {
    aspect-ratio: 2 / 3;
    overflow: hidden;
    border-radius: toRem(8);
    background-color: #f0f0f0;
    margin-bottom: toRem(15);

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }

  h3 {
    @include adaptiveValue("font-size", 20, 16);
    margin-bottom: toRem(10);
    font-weight: 700;
    overflow: hidden;
  }

  p {
    line-height: 1.4;
    color: #667;
    font-size: toRem(14);
  }
}

.card__no-image {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  color: #999;
  font-size: toRem(12);
}
</style>