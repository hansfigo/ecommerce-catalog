<template>
    <h1 :class="{'men' : isMen, 'woman' : !isMen}"> {{ title }}</h1>
</template>

<script>
export default {
    name: 'ProductTitle',
    props: {
        title : String,
        isMen : Boolean
    },
}

</script>

<style scoped>
.men{
    color:  var(--blue);
}

.woman {
    color: var(--purple);
}

h1{
    text-align: left;
} 
</style>