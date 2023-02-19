<script setup>
import { useFavoritosStore } from '@/store/favoritos.js'
import { storeToRefs } from 'pinia';

const useFavoritos = useFavoritosStore()
const { favoritos } = storeToRefs(useFavoritos)
const { remove } = useFavoritos
</script>
<template>
    <h1>favoritos</h1>
    <p v-if="favoritos.length === 0">Sin Favoritos</p>
    <ul class="list-group" v-else>
        <li class="list-group-item" v-for="poke in favoritos" :key="poke.id">
            <div>{{ poke.name }}</div>
            <div>
                <RouterLink :to="`/pokemons/${poke.name}`" class="me-2">Mas Info</RouterLink>
                <button class="btn btn-danger btn-sm" @click="remove(poke.id)">Eliminar</button>
            </div>
        </li>
    </ul>
</template>