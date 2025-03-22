<template>
    <div class="landscape-wall">
      <swiper :modules="modules" :slides-per-view="1" :loop="true" :autoplay="{ delay: 3000 }">
        <template #slides>
          <swiper-slide v-for="(photo, index) in landscapePhotos" :key="index">
            <img :src="photo.url" alt="Landscape" @click="showPhotoDetails(photo)" />
            <div class="photo-actions">
              <button @click="likePhoto(photo)">Like</button>
              <button @click="collectPhoto(photo)">Collect</button>
              <button @click="sharePhoto(photo)">Share</button>
            </div>
          </swiper-slide>
        </template>
      </swiper>
      <div v-if="selectedPhoto" class="photo-details">
        <h2>Photo Details</h2>
        <p>Location: {{ selectedPhoto.location }}</p>
        <p>Photographer: {{ selectedPhoto.photographer }}</p>
        <button @click="closePhotoDetails">Close</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import { Autoplay } from 'swiper/modules';
  import 'swiper/css';
  import 'swiper/css/autoplay';
  
  const modules = [Autoplay];
  
  const landscapePhotos = [
    {
      url: 'https://example.com/landscape1.jpg',
      location: 'Paris, France',
      photographer: 'John Doe'
    },
    // 更多照片...
  ];
  
  const selectedPhoto = ref(null);
  
  const showPhotoDetails = (photo) => {
    selectedPhoto.value = photo;
  };
  
  const closePhotoDetails = () => {
    selectedPhoto.value = null;
  };
  
  const likePhoto = (photo) => {
    // 实现点赞逻辑
    console.log('Liked photo:', photo);
  };
  
  const collectPhoto = (photo) => {
    // 实现收藏逻辑
    console.log('Collected photo:', photo);
  };
  
  const sharePhoto = (photo) => {
    // 实现分享逻辑
    console.log('Shared photo:', photo);
  };
  </script>
  
  <style scoped>
  .landscape-wall {
    position: relative;
  }
  
  .landscape-wall img {
    width: 100%;
    height: auto;
  }
  
  .photo-actions {
    position: absolute;
    bottom: 10px;
    left: 10px;
  }
  
  .photo-details {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: white;
    padding: 20px;
    border: 1px solid #ccc;
    z-index: 100;
  }
  </style>