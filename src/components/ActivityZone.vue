<template>
    <div class="activity-zone">
      <h2>Activity Zone</h2>
      <div class="filters">
        <select v-model="selectedType">
          <option value="">All Types</option>
          <option value="lecture">Lecture</option>
          <option value="workshop">Workshop</option>
          <option value="travel">Travel</option>
        </select>
        <!-- 更多筛选条件 -->
      </div>
      <div class="activity-cards">
        <div class="activity-card" v-for="activity in filteredActivities" :key="activity.id">
          <h3>{{ activity.title }}</h3>
          <p>Time: {{ activity.time }}</p>
          <p>Location: {{ activity.location }}</p>
          <p>{{ activity.description }}</p>
          <button @click="openRegistration(activity)">Register</button>
        </div>
      </div>
      <div v-if="registrationActivity" class="registration-form">
        <h2>Register for {{ registrationActivity.title }}</h2>
        <input type="text" v-model="name" placeholder="Name" />
        <input type="email" v-model="email" placeholder="Email" />
        <button @click="submitRegistration">Submit</button>
        <button @click="closeRegistration">Cancel</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue';
  
  const activities = [
    {
      id: 1,
      title: 'Web Development Workshop',
      time: '2025-03-20 10:00',
      location: 'Online',
      description: 'Learn web development skills from experts.',
      type: 'workshop'
    },
    // 更多活动...
  ];
  
  const selectedType = ref('');
  
  const filteredActivities = computed(() => {
    if (selectedType.value === '') {
      return activities;
    }
    return activities.filter(activity => activity.type === selectedType.value);
  });
  
  const registrationActivity = ref(null);
  const name = ref('');
  const email = ref('');
  
  const openRegistration = (activity) => {
    registrationActivity.value = activity;
  };
  
  const closeRegistration = () => {
    registrationActivity.value = null;
  };
  
  const submitRegistration = () => {
    // 实现报名逻辑
    console.log('Registered for:', registrationActivity.value.title);
    console.log('Name:', name.value);
    console.log('Email:', email.value);
    closeRegistration();
  };
  </script>
  
  <style scoped>
  .activity-zone {
    padding: 20px;
  }
  
  .filters {
    margin-bottom: 20px;
  }
  
  .activity-cards {
    display: flex;
    flex-wrap: wrap;
  }
  
  .activity-card {
    width: 300px;
    margin: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    background-color: white;
  }
  
  .registration-form {
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