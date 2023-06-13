<template>
  <div class="resultContainer" id="resultContainer">
    <DrugView 
        v-for="drug in results"
        :key="drug.id"
        :props="drug"
    />
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue';
import DrugView from "./DrugView.vue";
import { type DrugProp } from '@/Drug.type';

defineProps<{
  results: DrugProp[]
}>();

</script>

<style></style>
