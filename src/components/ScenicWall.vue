<template>
    <div class="photo-wall">
      <!-- 布局切换按钮 -->
      <div class="layout-switch">
        <button @click="layout = 'carousel'">轮播图</button>
        <button @click="layout = 'waterfall'">瀑布流</button>
      </div>
  
      <!-- 轮播图模式 -->
      <Swiper v-if="layout === 'carousel'" 
              :modules="[SwiperAutoplay]"
              :slides-per-view="1"
              :loop="true"
              :autoplay="true">
        <SwiperSlide v-for="photo in photos" :key="photo.id">
          <img :src="photo.url" alt="风景图片">
          <div class="photo-info">
            <h3>{{ photo.title }}</h3>
            <p>{{ photo.location }}</p>
            <div class="actions">
              <button @click="likePhoto(photo.id)">❤️ {{ photo.likes }}</button>
              <button @click="sharePhoto(photo)">↗️ 分享</button>
            </div>
          </div>
        </SwiperSlide>
      </Swiper>
  
      <!-- 瀑布流模式 -->
      <Masonry v-if="layout === 'waterfall'"
               :cols="{ default: 3, 800: 2, 500: 1 }"
               :gutter="20">
        <div v-for="photo in photos" :key="photo.id" class="masonry-item">
          <img :src="photo.url" alt="风景图片" @click="showDetail(photo)">
          <!-- 悬浮信息层 -->
        </div>
      </Masonry>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { usePhotoStore } from '@/stores/photos';
  
  // 使用 Pinia 状态管理
  const photoStore = usePhotoStore();
  const { photos } = storeToRefs(photoStore);
  
  const layout = ref('carousel');
  
  const likePhoto = (id) => {
    photoStore.likePhoto(id);
  };
  
  const showDetail = (photo) => {
    // 显示模态框展示详细信息
  };
  </script>