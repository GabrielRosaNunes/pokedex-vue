<script setup>
import PageTitle from '@/components/PageTitle.vue'
import Pokedex from '@/components/Pokedex.vue'
</script>

<template>
    <div>
      <nav class="navbar">
        <PageTitle title="Pokedéx"></PageTitle>
      </nav>
      <Pokedex></Pokedex>
    </div>
</template>

<style scoped>
  nav {
    text-align: center;
    padding: 30px
  }
</style>