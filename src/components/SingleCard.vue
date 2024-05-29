<script>
export default {
    name: 'SingleCard',
    props: {
        // Definisce che la prop card è un oggetto
        card: Object,
    },
};
</script>
<template>
    <div class="card">

        <img :src="card.card_images[0].image_url" />
        <h2>{{ card.name }}</h2>
        <p><strong>{{ card.archetype }}</strong> </p>
    </div>
</template>

<style scoped>
.card {
    border: 1px solid #ccc;
    padding: 1rem;
    margin: 1rem;
    text-align: center;
    background-color: #fff;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}


.card img {
    max-width: 100%;
    height: auto;
    margin-bottom: 1rem;
}
</style>