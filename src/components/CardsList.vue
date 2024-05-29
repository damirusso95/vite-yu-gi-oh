<script>
import SingleCard from './SingleCard.vue';
import { store } from '../store.js';
import axios from 'axios';

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
    computed: {
        filteredCards() {
            if (this.selectedArchetype === '') {
                return this.cards;
            }
            return this.cards.filter(card => card.archetype === this.selectedArchetype);
        }
    },
    methods: {
        filterCards() {
            this.cards = store.carte.filter(card => {
                return this.selectedArchetype === '' || card.archetype === this.selectedArchetype;
            });
        }
    },
    mounted() {
        axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
            .then(response => {
                store.carte = response.data.data;
                this.cards = store.carte;
            })
            .catch(error => {
                console.error('Errore durante il recupero dei dati:', error);
            });
    }
};
</script>

<template>
    <div class="container">
        <div class="cards-list">
            <SingleCard v-for="(card, index) in filteredCards" :key="index" :card="card" />
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