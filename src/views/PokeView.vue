<script setup>
import { useRoute, useRouter } from "vue-router";
import { useGetData } from "../composables/getData";

const { data, getData, loading, error } = useGetData()

const route = useRoute()
const router = useRouter()

const back = () => {
    router.push("/pokemons");
};

// const getData = async () => {
//     console.log(route.params.name);
//     try {
//         const { data } = await axios.get(
//             `https://pokeapi.co/api/v2/pokemon/${route.params.name}`
//         );
//         pokeSprite.value = data.sprites.front_default;
//     } catch (error) {
//         console.log(error);
//         pokeSprite.value = null;
//     }
// };

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
</script>
<template>
    <main class="text-center">
        <p v-if="loading">Cargando Informacion ...</p>
        <div class="alert alert-danger mt-2" v-if="error">No existe el pokemon</div>
        <div v-if="data">
            <img :src="data.sprites?.front_default" alt="" />
            <h1>Poke: {{ $route.params.name }}</h1>
        </div>
        <button class="btn btn-outline-primary" @click="back()">Volver al listado</button>
    </main>
</template>
