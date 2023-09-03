<template>
    <h1 :class="{ 'men': isMen, 'woman': !isMen }">${{ price }}</h1>
</template>

<script>
export default {
    name: 'PriceTag',
    props: {
        price: Number,
        isMen : Boolean
    },
}
</script>

<style scoped>
h1 {
    font-size: 1.8rem;
    text-align: left;
}

.men {
    color: var(--blue);
}

.woman {
    color: var(--purple);
}
</style>