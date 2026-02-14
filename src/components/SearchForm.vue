<script setup>
const model = defineModel()

const emit = defineEmits(['search'])

const handleSubmit = () => {
  emit('search')
}
</script>

<template>
  <form @submit.prevent="handleSubmit" class="search-form">
    <input 
      v-model="model" 
      type="text" 
      placeholder="Type movie title..."
    >
    <button type="submit">Search</button>
  </form>
</template>

<style lang="scss" scoped>
@use '../assets/mixins' as *;

.search-form {
  display: flex;
  gap: toRem(10);
  margin-bottom: toRem(30);
  
  input {
    flex: 1;
    padding: toRem(12) toRem(20);
    border-radius: toRem(8);
    border: 1px solid #ccc;
    font-size: toRem(16);
    outline: none;
    &:focus { border-color: #000; }
  }

  button {
    padding: toRem(12) toRem(25);
    background-color: #000;
    color: white;
    border: none;
    border-radius: toRem(8);
    cursor: pointer;
    font-weight: bold;
    &:hover { background-color: #35495e; }
  }
}
</style>