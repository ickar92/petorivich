<template>
  <div id="app">
    <product-card :product="product"
      v-for="(product, index) in products"
      photoModifier="_220x220_1"
      :key="index"></product-card>
  </div>
</template>

<script>
import ProductCard from './components/ProductCard.vue'
import http from './http'

export default {
  name: 'app',
  components: { ProductCard },

  data () {
    return {
      products: []
    }
  },

  created () {
    this.getProducts()
      .then(products => {
        this.products = products
      })
      .catch(err => {
        console.error(err)
      })
  },
    
  methods: {
    getProducts() {
      return http.get('/products').then(res => res.data)
    }
  }
}
</script>
