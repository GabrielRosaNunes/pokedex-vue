<script setup>
import { onMounted, reactive, ref } from "vue";
import axios from "axios";

    const pokemonData = ref(undefined)
    const props = defineProps({
        name:String,
        image:String
    });

    const state = reactive({
        pokemonData
    })

    function getPokemon() {
        axios.get(props.image).then(
            (response) => {
                state.pokemonData = response.data
            }
        )
    }

    onMounted(() => {
        getPokemon();
    })

</script>

<template>
    <div v-if="pokemonData != undefined" class="PokemonCard" >
        <img  :src="pokemonData.sprites.other.home.front_default" :alt="props.name" width="200" height="200" />
        <h3 >{{ pokemonData.name }}</h3>
    </div>
</template>

<style scoped>
    .PokemonCard {
        border-radius:35px;
        background-color:rgb(241, 241, 241);
        display: flex;
        flex-direction: column;
        align-items: center;
        -webkit-box-shadow: 5px 5px 14px 4px rgba(0,0,0,0.35); 
        box-shadow: 5px 5px 14px 4px rgba(0,0,0,0.12);
        max-height: 144px;
        margin-top: 118px;
    }

    h3 {
        font-family: 'Roboto';
        text-transform: capitalize;
        padding: 17px;
        padding-bottom: 41px;
    }

    .PokemonCard:hover {
        background-color: rgb(212, 211, 211);
        cursor:pointer;
    }

    img,h3 {
        position: relative;
        top: -85%;
    }
</style>