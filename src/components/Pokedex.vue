<script setup>
    import { reactive,onMounted,ref } from "vue";
    import axios from 'axios';
    import PokemonCard from "./PokemonCard.vue";
    import PokemonModal from "./PokemonModal.vue";

    const isPokemonModalActive = ref(false);
    const urlPokemon = ref('');
    const pokemons = ref([])
    const state = reactive({pokemons});
    
    const loading = reactive({
        status:false
    });

    function openModal(url) {
        urlPokemon.value = url
        isPokemonModalActive.value = true
    }

    function loadPokemons() {
        axios.get('https://pokeapi.co/api/v2/pokemon/?limit=25')
        .then((response) => {
            console.log(response.data)
            state.pokemons =  response.data.results;
        });
    }

    onMounted(() => {
        loadPokemons();
        
    })
</script>

<template>
    <div class="container-grid">
        <PokemonCard @click="openModal(pokemon.url)" v-for="(pokemon,index) in pokemons" :key="index" :name="pokemon.name"
        :image="pokemon.url" 
        ></PokemonCard>
    </div>
    <PokemonModal v-if="isPokemonModalActive" @closeModal="isPokemonModalActive = false" :url="urlPokemon"></PokemonModal>
</template>

<style scoped>
    .container-grid {
        padding:10px;
        width: 80%;
        margin: 0 auto;
        display: grid;
        grid-gap:20px;
        grid-template-columns: 1fr 1fr 1fr 1fr 1fr ;
        
    }
</style>