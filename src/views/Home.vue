<template>
  <div class="home">
    <h1>Mon super jeu de la mort qui tue</h1>
    <router-link :to="{ path: '/start'}">Commencer la partie</router-link>
  </div>
</template>

<script>

export default {
  name: 'home',
}
</script>
