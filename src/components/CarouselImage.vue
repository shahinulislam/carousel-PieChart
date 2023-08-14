<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue';
const items = ref([
  'https://images.unsplash.com/photo-1499951360447-b19be8fe80f5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80',
  'https://images.unsplash.com/photo-1508717272800-9fff97da7e8f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1171&q=80',
  'https://images.unsplash.com/photo-1495195129352-aeb325a55b65?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1176&q=80',
  'https://images.unsplash.com/photo-1497864149936-d3163f0c0f4b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1169&q=80',
  'https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80',
  'https://images.unsplash.com/photo-1507525428034-b723cf961d3e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1473&q=80',
])

let carousel = null

const newItem = ref('https://images.unsplash.com/photo-1614082242765-7c98ca0f3df3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80')

function addNewitem() {
  items.value.push(newItem.value);
  destroyCarousel();
  nextTick(() => {
    initializeCarousel();
  });
}

function initializeCarousel() {
  carousel = new Flickity('#carousel', {});
}

function destroyCarousel() {
  if (carousel) {
    carousel.destroy();
    carousel = null;
  }
}

onMounted(() => {
  initializeCarousel();
});

onBeforeUnmount(() => {
  destroyCarousel();
});

</script>

<template>

  <div class="my-10">
    <!-- <input type="text" v-model="newItem"> -->
    <button @click="addNewitem()" class="ml-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Add New Image
    </button>

  </div>
  <div class="mx-auto items" id="carousel">
    <div :style="`background-image:url(${item})`" class="item" v-for="item, index in items" :key="item">{{ index + 1 }}</div>
  </div>
</template>

<style scoped>
.items {
  width: 600px;
  height: 400px;
}
.item {
  width: 500px;
  height: 400px;
  background-size: cover;
}
</style>
