<script setup lang='ts'>
import { IEmployees } from '../models/IEmployees';

interface IEmployeeCardProps {
  employee: IEmployees;
}

defineProps<IEmployeeCardProps>();
</script>

<template>
  <h3>{{ employee.first_name }}</h3>
  <div>
    <img :src="employee.avatar" :alt="employee.first_name" />
  </div>

</template>

<style scoped></style>