<template>
    <div class="rating">
        <p>{{ rating }}/5</p>
        <div class="bar">
            <div v-for="i in roundedRating" :key="`${i}a`">
                <div class="circle-filled" :class="{ 'man-circle': isMen, 'woman-circle': !isMen }">

                </div>
            </div>
            <div v-for="i in 5-roundedRating" :key="`${i}b`">
                <div class="circle-border" :class="{ 'man-circle-border': isMen, 'woman-circle-border': !isMen }">

                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'RatingBar',
    props: {
        rating: Number,
        isMen: Boolean
    },
    computed: {
    roundedRating() {
      // Menggunakan Math.round() untuk membulatkan nilai rating
      return Math.round(this.rating);
    }
  }
}
</script>


<style scoped>
.rating {
    display: flex;
    gap: 1rem;
    align-items: center;
}

.circle-filled {
    height: 1.2rem;
    width: 1.2em;
    border-radius: 200px;
}

.circle-border {
    height: 1.2rem;
    width: 1.2em;
    border-radius: 200px;
}

.man-circle {
    background-color: var(--blue);
}

.woman-circle {
    background-color: var(--purple);

}

.man-circle-border{
    border: 1px solid var(--blue);

}

.woman-circle-border{
    border: 1px solid var(--purple);
}

.bar {
    display: flex;
    gap: 0.2rem;
}
</style>