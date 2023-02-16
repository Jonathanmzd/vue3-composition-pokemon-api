<script setup>
import axios from "axios";
import { ref } from "vue";
import { RouterLink } from "vue-router";

// Const de array 
const pokemons = ref([]);

const getData = async () => {
    try {
        const { data } = await axios.get("https://pokeapi.co/api/v2/pokemon");
        pokemons.value = data.results;
    } catch (error) {
        console.log(error);
    }
}

getData();
</script>

<template>
    <div class="container">
        <h1>pokemons</h1>
        <ul>
            <li v-for="(item, index) in pokemons">
                <RouterLink :to="`/pokemons/${item.name}`">{{ item.name }}</RouterLink>
            </li>
        </ul>
    </div>
</template>