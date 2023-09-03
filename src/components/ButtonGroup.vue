<template>
    <div>
        <button :class="{ 'men': isMen, 'woman': !isMen }">Buy Now</button>
        <button :class="{ 'next-men': isMen, 'next-woman': !isMen }" :disabled="isLoading"
            @click="nextProduct">Next</button>
    </div>
</template>

<script>
export default {
    name: 'ButtonGroup',
    props: {
        isLoading: Boolean,
        nextProduct: Function,
        isMen: Boolean
    },
    methods: {
        callNextProduct() {
            this.nextProduct()
        }
    }
}

</script>

<style scoped>
div {
    display: flex;
    gap: 2rem;
    width: 100%;
}

button {
    display: flex;
    width: 100%;
    padding: 0.6rem 0rem 0.6rem 0rem;
    border-radius: 0.4rem;
    color: white;
    justify-content: center;
    font-size: 1rem;
    cursor: pointer;
    transition: all 500ms ease-in-out;

}

next-button {
    display: flex;
    width: 100%;
    padding: 0.6rem 0rem 0.6rem 0rem;
    border-radius: 0.4rem;
    justify-content: center;
    background-color: white;
    font-size: 1rem;
    border: 3px solid rgba(114, 0, 96, 1);
    cursor: pointer;
    transition: all 500ms ease-in-out;
}

next-button:hover {
    background-color: rgb(163, 163, 163);
}

.next-men {
    border-color: rgba(0, 39, 114, 1);
    color: rgba(0, 39, 114, 1);
}

.next-woman {
    border-color: rgba(114, 0, 96, 1);
    color: rgba(114, 0, 96, 1);
}

.men {
    background-color: rgba(0, 39, 114, 1);
}

.woman {
    background-color: rgba(114, 0, 96, 1);
}


@media (max-width: 640px) {
    div {
        gap: 1rem;
        flex-direction: column;
    }
}
</style>