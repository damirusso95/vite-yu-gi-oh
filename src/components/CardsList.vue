
<script>
// Import componente SingleCard
import SingleCard from './SingleCard.vue';
// import store
import { store } from '../store.js';

export default {
    name: 'CardsList',
    components: {
        SingleCard,
        
    },
    data() {
        return {
            // Usa i dati dello store
      cards: store.carte,
        };
    },
};
</script>

<template>
    <div class="container">
        <div class="cards-list">
            <!-- Itero attraverso l'array di dati e passa ogni elemento al componente SingleCard -->
            <SingleCard v-for="(card, index) in cards" :key="index" :card="card" />
        </div>
    </div>
</template>

<style scoped>
/* Spaziatura tra le carte */
.cards-list {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
    
}

.cards-list>* {
    flex: 1 1 calc(15% - 16px);
    box-sizing: border-box;
    
}

.container{
    background-color: burlywood;
    margin-top: 2rem;
    border-radius:10px;
}
</style>