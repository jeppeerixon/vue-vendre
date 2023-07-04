<script setup lang="ts">
import axios from 'axios';
import { ref, onMounted } from 'vue'
import { IEmployees } from './models/IEmployees';
import EmployeeCard from './components/EmployeeCard.vue'

  const employees = ref<IEmployees[]>([])
  const BASE_URL: string = 'https://reqres.in/api/users'

  const fetchData = async (): Promise<IEmployees[]> => {
    let response = await axios.get(`${BASE_URL}`);
    return response.data.data
  };

  onMounted(async () => {
    employees.value = await fetchData()
    console.log(employees.value)
  });

</script>

<template>
  <header>
    <h1>Buisness AB</h1>
  </header>
  <main>
    <EmployeeCard v-for="employee in employees" :employee="employee" :key="employee.id" />
  </main>
</template>

<style scoped>

  header {
    display: flex;
    align-items: start;
  }

  main {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
  }
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.vue:hover {
    filter: drop-shadow(0 0 2em #42b883aa);
  }
</style>
