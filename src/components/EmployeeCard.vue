<template>
  <div class="employeeCard">
    <img :src="employee.avatar" :alt="employee.first_name" />
    <hr>
    <h5>{{ employee.first_name }} {{ employee.last_name }}</h5>  
    <button><a :href="'mailto:' + employee.email">Contact</a></button>
  </div>

</template>

<script setup lang='ts'>
import { IEmployees } from '../models/IEmployees';

  interface IEmployeeCardProps {
    employee: IEmployees;
  }

  defineProps<IEmployeeCardProps>();
</script>

<style scoped>

.employeeCard {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
  border-radius: 0.5rem;
  background-color: #AEE2FF;
  padding: 1rem;
  box-shadow: 5px 5px 8px 1px rgba(0, 0, 0, 0.1);
}

h5 {
  margin: 0.5rem;
}

hr {
  width: 100%;
  height: 0.15rem;
  background-color: #b899ffc5;
  border-width: 0;
}

img {
  aspect-ratio: 1 / 1;
  height: 128px;
  border-radius: 50%;
}

a:any-link {
  color: #9c72ff;
}

</style>