<template>
  <header>
    <h1>Employees</h1>
  </header>
  <main>
    <EmployeeCard v-if="fetchSuccess" v-for="employee in employees" :employee="employee" :key="employee.id" />
    <div v-else>Failed to fetch data... please come back later!</div>
  </main>
  <footer>
    <button v-for="i in pages" :key="i" @click="handleClick">
      {{ i }}
    </button>
  </footer>
</template>

<script setup lang="ts">
import axios from 'axios';
import { ref, onMounted } from 'vue'
import { IEmployees } from './models/IEmployees';
import EmployeeCard from './components/EmployeeCard.vue'

  const employees = ref<IEmployees[]>([])
  const pages = ref<number>(0)
  const BASE_URL: string = 'https://reqres.in/api/users'
  const PAGE_URL: string = 'https://reqres.in/api/users?page='
  let fetchSuccess: boolean = true;

  const fetchData = async (url: string): Promise<IEmployees[]> => {
    try {
      let response = await axios.get(`${url}`);
      return response.data.data
    }
    catch(error){
      console.log(error)
      fetchSuccess = false;
    };
    
  };

  const fetchPages = async (): Promise<number> => {
    let response = await axios.get(`${BASE_URL}`);
    return response.data.total_pages
  };

  const handleClick = async (e: Event) => {
    let pageNumber: string = ((e.target as HTMLInputElement).innerHTML)
    employees.value = await fetchData(PAGE_URL+pageNumber)
  }

  onMounted(async () => {
    employees.value = await fetchData(BASE_URL)
    pages.value = await fetchPages()
  });
  

</script>

<style scoped>

  header {
    display: flex;
    align-items: start;
  }

  main {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    margin-bottom: 1rem;
  }

  button {
    margin-right: 1rem;
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
