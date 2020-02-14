<template>
  <div id="app">
    <b-container>
      <Home />
      <Filmes/>
    </b-container>
  </div>
</template>

<script>
import Home from './components/Home.vue'
import Filmes from './components/Filmes.vue'


export default {
  name: 'App',
  components: {
    Home,
    Filmes
  }
}
</script>

<style>

</style>
