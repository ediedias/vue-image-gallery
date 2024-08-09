<script setup>
import { ref } from 'vue';

const showModal = ref(false);
const currentImageIndex = ref(0);

const images = ref([
  'https://via.placeholder.com/600x400/0000FF/808080?text=Image+1',
  'https://via.placeholder.com/600x400/FF0000/FFFFFF?text=Image+2',
  'https://via.placeholder.com/600x400/FFFF00/000000?text=Image+3',
  'https://via.placeholder.com/600x400/00FF00/0000FF?text=Image+4',
  'https://via.placeholder.com/600x400/FF00FF/000000?text=Image+5',
  'https://via.placeholder.com/600x400/00FFFF/FF0000?text=Image+6',
  'https://via.placeholder.com/600x400/FF0000/FFFFFF?text=Image+7',
  'https://via.placeholder.com/600x400/00FF00/000000?text=Image+8',
]);

const openModal = (index) => {
  currentImageIndex.value = index;  
  showModal.value = true;
}

const closeModal = () => {
  showModal.value = false;
}

const prevImage = () => {
  currentImageIndex.value = (currentImageIndex.value - 1 + images.value.length) % images.value.length;
}

const nextImage = () => {
  currentImageIndex.value = (currentImageIndex.value + 1) % images.value.length;
};

</script>

<template>
  <div class="container mx-auto p-4">
    <h1 class="text-3xl font-bold mb-6 text-center">Image Gallery</h1>
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
      <div 
        v-for="(image, index) in images"
        :key="index"
        class="cursor-pointer"
        @click="openModal(index)">
        <img :src="image" class="w-full h-48 object-cover rounded-lg shadow-lg" />
      </div>
    </div>

    <div v-if="showModal" class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50">
      <div class="relative">
        <button @click="closeModal" class="absolute top-0 right-0 m-2 text-white text-xl">&times;</button>
        <button @click="prevImage" class="absolute left-0 top-1/2 transform -translate-y-1/2 text-white text-xl">&lt;</button>
        <button @click="nextImage" class="absolute right-0 top-1/2 transform -trsnlate-y-1/2 text-white text-xl">&gt;</button>
        <img :src="images[currentImageIndex]" class="max-w-full max-h-screen object-contain rounded-lg shadow-lg" />
      </div>
    </div>
  </div>
</template>