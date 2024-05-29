<script>
import CardsList from './components/CardsList.vue';
import AppHeader from './components/AppHeader.vue';
import axios from 'axios';
import { store } from './store.js';

export default {
  name: 'App',
  components: {
    CardsList,
    AppHeader
  },
  data() {
    return {
      archetypes: store.archetipi,
      selectedArchetype: ''  // Mantiene l'archetipo selezionato
    };
  },
  created() {
    // Chiamata axios per recuperare gli archetipi
    axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php')
      .then(response => {
        // Aggiorna lo store con gli archetipi recuperati
        store.archetipi = response.data.map(archetype => archetype.archetype_name);
        this.archetypes = store.archetipi;
      })
      .catch(error => {
        console.error('Errore durante il recupero degli archetipi:', error);
      });

    // Chiamata axios per recuperare le carte
    axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
      .then(response => {
        store.carte = response.data.data;
      })
      .catch(error => {
        console.error('Errore durante il recupero delle carte:', error);
      });
  },
  methods: {
    filterCardsByArchetype() {
      // Questo metodo verrà chiamato quando l'utente cambia l'archetipo selezionato
      this.$refs.cardsList.filterCards();
    }
  }
};
</script>
<template>
  <div id="app">
    <AppHeader />
    <div>
      <label for="archetype">Filter by Archetype:</label>
      <select id="archetype" v-model="selectedArchetype" @change="filterCardsByArchetype">
        <option value="">All</option>
        <option v-for="archetype in archetypes" :key="archetype" :value="archetype">
          {{ archetype }}
        </option>
      </select>
    </div>
    <CardsList :selectedArchetype="selectedArchetype" ref="cardsList" />
  </div>
</template>

<style>
body {
  background-color: rgb(165, 106, 46);
}
</style>
