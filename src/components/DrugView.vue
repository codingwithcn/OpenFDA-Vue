<template>
    <div class="result" :id="props.id">
        <div class="header">
            <div>{{ props.openfda.brand_name[0] }}</div>
            <div class="status">{{ props.openfda.manufacturer_name[0] }} / {{ props.openfda.generic_name[0] }}</div>
        </div>
        <div class="description">
            <div class="section close">
                <div class="title" onclick="this.parentElement.classList.toggle('close')">Purpose</div>
                <ul class="list">
                    <li
                        v-for="(purpose, index) in props.purpose"
                        :key="index"
                    >{{ purpose }} </li>
                </ul>
            </div>

            <div class="section close">
                <div class="title" onclick="this.parentElement.classList.toggle('close')">Indications Usuage</div>
                <ul class="list">
                    <li
                        v-for="(purpose, index) in props.indications_and_usage"
                        :key="index"
                    >{{ purpose }} </li>
                </ul>
            </div>

            <div class="section close">
                <div class="title" onclick="this.parentElement.classList.toggle('close')">Dosage & Administration</div>
                <ul class="list">
                    <li
                        v-for="(purpose, index) in props.dosage_and_administration"
                        :key="index"
                    >{{ purpose }} </li>
                </ul>
            </div>

            <div class="section close">
                <div class="title" onclick="this.parentElement.classList.toggle('close')">Active Ingredient</div>
                <ul class="list">
                    <li
                        v-for="(purpose, index) in props.active_ingredient"
                        :key="index"
                    >{{ purpose }} </li>
                </ul>
            </div>

            <div class="section close">
                <div class="title" onclick="this.parentElement.classList.toggle('close')">Warnings</div>
                <ul class="list">
                    <li
                        v-for="(purpose, index) in props.warnings"
                        :key="index"
                    >{{ purpose }} </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";
import { type DrugProp } from '@/Drug.type';

defineProps<{ props: DrugProp }>()

</script>

<style scoped>
.result {
    width: 50vw;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid gainsboro;
    border-radius: 10px;
    padding: 10px;
    margin-top: 10px;
    margin-bottom: 10px;
}

.result .header {
    border-bottom: 1px solid gainsboro;
    margin-bottom: 10px;
    padding-bottom: 10px;
    display: flex;
    justify-content: space-between;
}

.result .header .status {
    border-radius: 10px;
    background: green;
    padding: 10px;
    color: white;
}

.result .description .section {
    border: 1px solid gainsboro;
    border-radius: 10px;
    padding: 10px;
    margin-top: 10px;
    margin-bottom: 10px;
}

.result .description .section .title {
    background: gainsboro;
    border-radius: 10px;
    padding: 10px;
    cursor: pointer;
}

.result .description .section.close .list {
    display: none;
}

</style>
