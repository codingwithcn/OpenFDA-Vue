<script setup lang="ts">
import { ref, watchEffect } from 'vue';

import ResultContainer from './components/ResultContainer.vue';

import data from '@/acetaminophen_results'

import { type DrugProp } from '@/Drug.type';

const resultRef = ref<{ result: DrugProp[] }>({ result: [] });
const searchText = ref("");

const searchDrugs = (drugSearch: string) => {
    resultRef.value.result = data.results.filter((drug) =>
      drugSearch.length > 1
        ? new RegExp(drugSearch, 'i').test(
            (() => {
              if (drug.openfda === undefined) return ''
              if (drug.openfda.brand_name === undefined) return ''
              return drug.openfda.brand_name ? drug.openfda.brand_name[0] : ''
            })()
          )
        : (() => drug.openfda !== undefined && drug.openfda.brand_name !== undefined)()
    ) as DrugProp[]
}

searchDrugs(searchText.value);

watchEffect( () => searchDrugs(searchText.value) )

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
