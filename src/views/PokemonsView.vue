<script setup>
import { RouterLink } from "vue-router";
import { useGetData } from "../composables/getData";

const { data, getData, loading, error } = useGetData()

// const getData = async () => {
//     try {
//         const { data } = await axios.get("https://pokeapi.co/api/v2/pokemon");
//         pokemons.value = data.results;
//     } catch (error) {
//         console.log(error);
//     }
// }

getData("https://pokeapi.co/api/v2/pokemon");
</script>

<template>
    <div class="container">
        <h1>pokemons</h1>
        <p v-if="loading">Cargando Informacion ...</p>
        <div class="alert alert-danger mt-2" v-if="error">{{ error }}</div>
        <div v-if="data">
            <ul class="list-group">
                <li class="list-group-item" v-for="(poke, index) in data.results">
                    <RouterLink :to="`/pokemons/${poke.name}`">{{ poke.name }}</RouterLink>
                </li>
            </ul>
            <div class="mt-2 mb-2">
                <button :disabled="!data.previous" class="btn btn-primary me-2" @click="getData(data.previous)">Previous</button>
                <button :disabled="!data.next" class="btn btn-primary" @click="getData(data.next)">Next</button>
            </div>
        </div>
    </div>
</template>