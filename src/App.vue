<script setup lang="ts">
import { ref, watchEffect } from 'vue';

import ResultContainer from './components/ResultContainer.vue';

import { type DrugProp } from '@/Drug.type';

const resultRef = ref<{ result: DrugProp[] }>({ result: [] });
const searchText = ref("");

const searchDrugs = async (drugSearch: string) => {
  if ( drugSearch.length > 0 ) {
    const res = await fetch(`https://api.fda.gov/drug/drugsfda.json?search=openfda.brand_name:'${drugSearch.replace(" ",  "+")}'&limit=1000`);

    if ( res.status == 200 ) {
      resultRef.value.result = ( await res.json() ).results;
    }else {
      resultRef.value.result = [];
    }
  }
}

searchDrugs(searchText.value);

</script>

<template>
  <div class="searchContainer">
    <input type="input" class="searchInput" id="searchInput" v-model="searchText" />
    <div class="searchButton" id="searchButton" @click="searchDrugs(searchText)">Search</div>
  </div>

  <ResultContainer :results="resultRef.result"/>
</template>

<style scoped>
.searchContainer {
  width: 50vw;
  margin-right: auto;
  margin-left: auto;
  display: flex;
}

.searchButton {
  cursor: pointer;
}

.searchContainer input {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 10px;
  width: 40vw;
  border-right: none;
  border-top-right-radius: 0px;
  border-bottom-right-radius: 0px;
}

.searchContainer div {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 10px;
  border-top-left-radius: 0px;
  border-bottom-left-radius: 0px;
}
</style>
