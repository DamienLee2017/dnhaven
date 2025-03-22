<template>
    <div class="culture-section">
      <section class="core-values">
        <h2>核心价值</h2>
        <div class="values-grid">
          <div v-for="value in values" 
               class="value-card"
               :style="{ backgroundColor: value.color }">
            <h3>{{ value.title }}</h3>
            <p>{{ value.description }}</p>
          </div>
        </div>
      </section>
  
      <section class="member-stories">
        <h2>成员故事</h2>
        <StoryCarousel :stories="stories" />
      </section>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const values = ref([
    {
      title: '自由',
      color: '#4CAF50',
      description: '支持灵活的工作生活方式...'
    },
    // 其他价值观数据...
  ]);
  
  const stories = ref([
    {
      author: '张三',
      avatar: '/avatars/1.jpg',
      content: '在社区中我找到了...'
    },
    // 其他故事数据...
  ]);
  </script>