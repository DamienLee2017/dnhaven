<!-- <script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <TheWelcome />
  </main>
</template> -->


<template>
  <div>
    <LandscapeWall />
    <ActivityZone />
    <CommunityCulture />
  </div>
</template>

<script setup>
import LandscapeWall from '../components/LandscapeWall.vue';
import ActivityZone from '../components/ActivityZone.vue';
import CommunityCulture from '../components/Community_Culture.vue';
</script>

<style scoped>
/* 全局样式 */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f4f4f4;
}
</style>