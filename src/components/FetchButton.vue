<script setup lang="ts">
import {ref} from "vue";

const rawData = ref([]);

interface Data {
    "message": string,
    "status": string
}

const fetchData = async (): Promise<Data> => {
    const response: any = await fetch("https://dog.ceo/api/breeds/image/random");
    const data: Data = await response.json();
    rawData.value = data;

    return data;
}
</script>

<template>
    <button class="fetch-button" @click=fetchData>
        FetchButton
    </button>

    <img class="dog-img" v-if="rawData && rawData.message" :src="rawData.message" alt="Dog Image">
</template>

<style lang="scss" scoped>
    .fetch-button {
        display: block;
        margin: 0 auto;
    }

    .dog-img {
        display: block;
        width: 100%;
    }
</style>