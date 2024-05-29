<script>
import SingleCard from './SingleCard.vue';
import { store } from '../store.js';

export default {
    name: 'CardsList',
    components: {
        SingleCard
    },
    props: {
        selectedArchetype: String // Riceve l'archetipo selezionato come prop
    },
    data() {
        return {
            cards: store.carte
        };
    },
    methods: {
        updateCards() {
            this.cards = store.carte;
        }
    },
    mounted() {
        this.updateCards();
    }
};
</script>
<template>
    <div class="container">
        <div class="cards-list">
            <SingleCard v-for="(card, index) in cards" :key="index" :card="card" />
        </div>
    </div>
</template>
<style scoped>
.cards-list {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
}

.cards-list>* {
    flex: 1 1 calc(15% - 16px);
    box-sizing: border-box;
}

.container {
    background-color: burlywood;
    margin-top: 2rem;
    border-radius: 10px;
}
</style>