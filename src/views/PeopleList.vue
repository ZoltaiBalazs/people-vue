<script setup lang="ts">
import PeopleCard from '@/components/PeopleCard.vue';
import data_people from '@/data/data_people';
import type People from '@/types/People';
import { ref, computed } from 'vue';

const people = ref<People[]>();
people.value = data_people.getPeople();
const sortOrder = ref<'asc' | 'desc'>('asc')
const sortProperty = ref<'last_name' | 'first_name'>('first_name');

const sortedPeople = computed(() => {
  return [...people.value].sort((a, b) => {
    const comparison = a[sortProperty.value].localeCompare(b[sortProperty.value]);
    return sortOrder.value === 'asc' ? comparison : -comparison;
  });
});

const setSortProperty = (property: 'last_name' | 'first_name') => {
  if (sortProperty.value === property) {
    sortOrder.value = sortOrder.value === 'asc' ? 'desc' : 'asc';
  } else {
    sortProperty.value = property;
    sortOrder.value = 'asc';
  }
};

</script>

<template>
  <div class="table-container">
    <h1 class="display-5">People List</h1>
    <table>
      <thead>
        <tr>
          <th>id</th>
          <th>avatar</th>
          <th @click="setSortProperty('first_name')" class="sortable-header">
            first name
          </th>
          <th @click="setSortProperty('last_name')" class="sortable-header">
            last name
          </th>
          <th>email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="person in sortedPeople" :key="person.id">
          <PeopleCard :person="person" />
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>

.table-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 20px;
}

h1.display-5 {
  margin-bottom: 20px;
  font-size: 2rem;
  text-align: center;
  color: #333;
}

table {
  width: 80%;
  max-width: 1200px;
  border-collapse: collapse;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

th,
td {
  padding: 12px;
  text-align: left;
}

th.sortable-header {
  cursor: pointer;
  position: relative;
  padding-right: 30px;
  transition: background-color 0.3s ease;
}

th.sortable-header:hover {
  background-color: #064f9c;
}

th {
  background-color: #007bff;
  color: white;
  font-weight: bold;
}

tbody tr:nth-child(odd) {
  background-color: #f9f9f9;
}

tbody tr:nth-child(even) {
  background-color: #e9e9e9;
}

tbody tr:hover {
  background-color: #e0e0e0;
}

.people-card img {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  object-fit: cover;
}

@media (max-width: 768px) {
  table {
    width: 100%;
    font-size: 14px;
  }

  th, td {
    padding: 8px;
  }
}
</style>