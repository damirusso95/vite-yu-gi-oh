

<script>
// Importa il componente CardsList
import CardsList from './components/CardsList.vue';
import AppHeader from  './components/AppHeader.vue';



export default {
  name: 'App',
  components: {
    CardsList,
    AppHeader
  },
};
</script>

<template>
  <div id="app">
    <AppHeader/>
    <CardsList />
  </div>
</template>

<style>
body{
  background-color: rgb(165, 106, 46);
}
</style>
