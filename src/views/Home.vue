<template>
  <div class="home">
    <div class="columns is-multiline">
      <div class="column is-12">
          <h2 class="is-size-2 has-text-centered">Products</h2>
      </div>

      <ProductBox 
        v-for="product in products"
        v-bind:key="product.id"
        v-bind:product="product" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'

import ProductBox from '@/components/ProductBox'

export default {
  name: 'Home',
  data() {
    return {
      products: []
    }
  },
  components: {
    ProductBox
  },
  mounted() {
    this.getProducts()

    document.title = 'Home | Cart Management'
  },
  methods: {
    async getProducts() {
      this.$store.commit('setIsLoading', true)

      await axios
        .get('/api/v1/products/')
        .then(response => {
          this.products = response.data
        })
        .catch(error => {
          console.log(error)
        })

      this.$store.commit('setIsLoading', false)
    }
  }
}
</script>