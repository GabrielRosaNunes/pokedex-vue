<script setup>
    import axios from 'axios';
    import { onMounted, ref } from 'vue';

    const isLoaded = ref(false);
    const props = defineProps({
        url:String
    });
    const pokemonData = ref({})

    const emit = defineEmits(['closeModal'])


    function click(event) {
        if (event.target.id == 'modal') {
            emit('closeModal')
        }
    }

    onMounted(() => {
        axios.get(props.url).then((response) => {
            console.log(response.data)
            pokemonData.value = response.data
        }).then(() => {
            isLoaded.value = true
        });
    })
</script>

<template>
    <transition name="fade">
        <div id="modal" class="Modal" @click="click">
            <div class="ModalContent">
                <div v-if="isLoaded">
                    <div class="modal-image">
                        <img  :src="pokemonData.sprites.other.home.front_default" :alt="props.name" width="200" height="200" />
                    </div>
                    <div class="pokemon-title">
                        <h2>{{ pokemonData.name }}</h2>
                    </div>
                    <div class="pokemon-stats">
                        <div class="pokemon-base-experience">
                            <div class="description">
                                Base Experience
                            </div>
                            <div class="value">
                                {{ pokemonData.base_experience }} exp
                            </div>
                        </div>
                        <div class="pokemon-height">
                            <div class="description">
                                Height
                            </div>
                            <div class="value">

                                {{ pokemonData.height }} m
                            </div>
                        </div>
                        <div class="pokemon-weight">
                            <div class="description">
                                Weight
                            </div>
                            <div class="value">

                                {{ pokemonData.weight }} Kg
                            </div>
                        </div>
                        <div class="pokemon-types">
                            <div class="description">
                                Types
                            </div>
                            <div class="value">
                                <p v-for="(type,index) in pokemonData.types" style="text-transform: capitalize;">
                                    {{ type.type.name }}
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
                <div v-else>
                    Carregando...
                    <br>
                    {{ props.url }}
                </div>
            </div>
        </div>
    </transition>
</template>

<style scoped>
    .Modal {
        width: 100%;
        height: 100%;
        background-color: #00000082;
        top: 0;
        position: fixed;
        left: 0;
        display:flex;
        justify-content: center;
        align-items: center;
        font-family: 'Roboto';
        
    }

    .ModalContent {
        width:50%;
        height: 80%;
        background-color:white;
        border-radius:40px;
        padding: 20px
    }
    .modal-image {
        text-align: center;
    }
    .modal-image > img {
        transform: translateY(-16px);
    }

    .pokemon-title {
        text-transform: capitalize;
        text-align: center;
    }

    .pokemon-stats {
        display: grid;
        grid-row-gap: 20px;
        grid-template-columns: 1fr 1fr;
    }
    .pokemon-base-experience {
        grid-column-start: 1;
        grid-column-end: 3;
    }
    .description {
        font-weight: bold;
    }
</style>