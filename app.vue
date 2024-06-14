<template>
  <div class="wrapper">
    <div v-for="(item, index) in items" :key="item.id" class="item">
      <h5>{{ item.title }}</h5>
      <img height="400" width="400" :src="item.url" :alt="item.title" :loading="index > 8 ? 'lazy' : 'eager'">
    </div>
  </div>
</template>
<script setup>

const items = ref([])
const {data} = await useAsyncData('items', () => fetch('https://jsonplaceholder.typicode.com/photos?_limit=100'), {transform: response => response.json()});
items.value = data.value
</script>
<style>
.wrapper {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}
.item {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

img {
  width: 100%;
  height: auto;
  object-fit: contain;
}

</style>
