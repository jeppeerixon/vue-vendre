<script setup lang="ts">
import axios from 'axios';
import { ref } from 'vue'
import { IEmployees } from "./models/IEmployees";

  const employees = ref<IEmployees[]>([])
  const BASE_URL: string = 'https://reqres.in/api/users'

  const fetchData = async (): Promise<IEmployees[]> => {
    let response = await axios.get(`${BASE_URL}`);
    return response.data
  };

  employees.value = await fetchData()


  console.log(employees.value)

</script>

<template>
  <p>hej</p>
</template>

<style scoped>
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
