<template>
  <div>
    <div :class="{ 'men-bg': isMen, 'woman-bg': !isMen }" class="bg">
    </div>
    <div class="main">
      <div v-if="!isLoading" class="card">
        <div class="image">
          <img :src="product.image" alt="">
        </div>
        <div class="info">
          <ProductTitle :title="product.title" :isMen="isMen" />
          <div class="row-2">
            <p>{{ product.category }}</p>
            <Rating :rating="rating" :isMen="isMen"/>
          </div>
          <hr>
          <p style="text-align: left; padding: 1rem 0rem 1rem 0rem;">{{ product.description }}</p>
          <hr>
          <Price :price="product.price" :isMen="isMen" />
          <ButtonGroup :nextProduct="nextProduct" :isLoading="isLoading" :isMen="isMen" />
        </div>
      </div>
      <div v-if="isLoading">
        <LoadingSpinner />
      </div>
      <div v-if="isError">
        Error
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import ButtonGroup from './ButtonGroup.vue'
import ProductTitle from './ProductTitle.vue'
import LoadingSpinner from './LoadingSpinner.vue'
import Price from './Price.vue'
import Rating from './Rating.vue'


export default {
  name: 'HomePage',
  components: {
    ButtonGroup,
    ProductTitle,
    LoadingSpinner,
    Price,
    Rating
  },
  props: {
    msg: String
  },
  data: function () {
    return {
      index: 1,
      product: {},
      rating: null,
      isError: false,
      isLoading: true,
      isMen: false, // Variabel boolean untuk menunjukkan apakah produk berkategori "men's clothing"
    }
  },
  methods: {
    async nextProduct() {
      this.isLoading = true

      if (this.index >= 20) {
        this.index = 0;
      }

      this.index++;

      const res = await fetch(`https://fakestoreapi.com/products/${this.index}`);
      const data = await res.json();

      // Validasi kategori produk
      if (data.category === "men's clothing" || data.category === "women's clothing") {
        this.product = data;
        const rating = data.rating;
        this.rating = rating.rate;

        // Mengatur isMen berdasarkan kategori
        this.isMen = data.category === "men's clothing";
      } else {
        // Jika kategori tidak sesuai, lanjut ke produk berikutnya
        this.nextProduct();
      }

      this.isLoading = false
    }
  },
  mounted: function () {
    this.isLoading = true

    const apiUrl = `https://fakestoreapi.com/products/${this.index}`;
    axios
      .get(apiUrl)
      .then(response => {
        const rating = response.data.rating
        this.product = response.data
        this.rating = rating.rate

        // Validasi kategori produk
        if (response.data.category === "men's clothing" || response.data.category === "women's clothing") {
          this.product = response.data;
          // Mengatur isMen berdasarkan kategori
          this.isMen = response.data.category === "men's clothing";
        } else {
          // Jika kategori tidak sesuai, lanjut ke produk berikutnya
          this.nextProduct();
        }
      })
      .catch(error => {
        console.error('Error ', error)
        this.isError = true
      })

    this.isLoading = false
  }
}
</script>




<style scoped>

hr{
  border-top: 1px solid var(--gray);
}
.bg {
  position: fixed;
  min-height: 50vh;
  width: 100%;
  z-index: 0;
  top: 0;
  left: 0;
  background: rgb(209, 209, 209);
}

.main {
  z-index: 10;
  display: flex;
  gap: 4rem;
  background: white;
  padding: 4rem;
  border-radius: 2rem;
  margin-left: 4rem;
  margin-right: 4rem;
  position: relative;
  box-shadow: 2px 4px 21px 0px rgba(0, 0, 0, 0.2);
  max-width: 1400px;
}

.card {
  z-index: 10;
  display: flex;
  gap: 4rem;
  justify-content: space-between;
  background: white;
  padding: 4rem;
  border-radius: 2rem;
  width: 100%;
  
}

.row-2 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.image {
  object-fit: cover;
  overflow: hidden;
  max-height: 22rem;
  min-width: 40%;
  background: rgb(213, 213, 213);
}

.image img {
  width: 100%;
  height: auto;
}

.men-bg {
    background-color: var(--light-blue);
}

.woman-bg {
    background-color: var(--light-purple);
}


@media (max-width: 1080px) { 
    .card{
        flex-direction: column;
        padding: 2rem;
    }

    .main{
      margin: 2rem;
    }
}

@media (max-width: 640px) { 
    .row-2{
      flex-direction: column;
    }
}


</style>
