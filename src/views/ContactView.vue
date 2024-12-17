<script setup lang="ts">
import { useRoute, useRouter } from 'vue-router';
import data_people from '@/data/data_people';
import { computed } from 'vue';

const route = useRoute();
const router = useRouter();

const personId = route.params.id;

const person = computed(() => {
  return data_people.getPeople().find((p) => p.id === Number(personId));
});

const goBack = () => {
  router.back();
};
</script>

<template>
    <div class="contact-view">
    <div class="contact-card" v-if="person">
      <img :src="person.avatar" alt="Avatar" class="avatar" />
      <h1>{{ person.first_name }} {{ person.last_name }}</h1>
      <p><strong>Email:</strong> {{ person.email }}</p>
    </div>
    <div v-else>
      <p>Person not found.</p>
    </div>
    <button class="back-button" @click="goBack">Go Back</button>
  </div>
</template>


<style scoped>
.contact-view {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.contact-card {
  text-align: center;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
  background-color: #f9f9f9;
}

.avatar {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  margin-bottom: 20px;
}

h1 {
  margin: 10px 0;
  font-size: 24px;
  color: #333;
}

p {
  margin: 5px 0;
  font-size: 18px;
  color: #555;
}

.back-button {
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.back-button:hover {
  background-color: #0056b3;
}
</style>