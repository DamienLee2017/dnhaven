<template>
    <div class="events-section">
      <div class="filters">
        <select v-model="selectedType">
          <option value="">全部类型</option>
          <option v-for="type in eventTypes" :value="type">{{ type }}</option>
        </select>
        <date-picker v-model="selectedDate" />
      </div>
  
      <div class="event-cards">
        <div v-for="event in filteredEvents" 
             class="event-card"
             :key="event.id">
          <h3>{{ event.title }}</h3>
          <p class="time">{{ formatDate(event.time) }}</p>
          <p class="location">{{ event.location }}</p>
          <button @click="showRegistration(event)">立即报名</button>
        </div>
      </div>
  
      <EventRegistrationModal 
        v-if="selectedEvent"
        :event="selectedEvent"
        @close="selectedEvent = null" />
    </div>
  </template>
  
  <script setup>
  import { computed, ref } from 'vue';
  import { useEventStore } from '@/stores/events';
  
  const eventStore = useEventStore();
  const { events } = storeToRefs(eventStore);
  
  const selectedType = ref('');
  const selectedDate = ref(null);
  const selectedEvent = ref(null);
  
  const filteredEvents = computed(() => {
    return events.value.filter(event => {
      const typeMatch = !selectedType.value || event.type === selectedType.value;
      const dateMatch = !selectedDate.value || 
                       new Date(event.time) >= selectedDate.value;
      return typeMatch && dateMatch;
    });
  });
  
  const showRegistration = (event) => {
    selectedEvent.value = event;
  };
  </script>