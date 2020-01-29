<template>
  <div>
    <h1>Product List</h1>
    <img
    v-if="loading"
    src="https://i.imgur.com/JfPpwOA.gif"
    >
    <ul v-else>
    <li v-for="product in products">
    {{product.title}} - {{product.price | currency}} - {{product.inventory}}
    <button
      :disabled="!productIsInStock(product)"
      @click="addProductToCart(product)"
      >Add to cart</button>
    </li>
    </ul>
  </div>
</template>

<script>
// import shop from '@/api/shop'
// import store from '@/store/index' > at last it is import in  main.js
import {mapState, mapGetters, mapActions} from 'vuex'

export default {
  data(){
    return {
      loading: false,
      productIndex: 1
    }
  },

  computed: {
    ...mapState({
    products: state => state.products
  }),

  ...mapGetters({
    productIsInStock: 'productIsInStock'
  })
  },
 /*  productIsInStock (){
      return this.$store.getters.productIsInStock
     }
   }, */

// computed: {
//     products (){
//       // return this.$store.getters.availableProducts
//       return this.$store.state.products
//     },

//     productIsInStock (){
//       return this.$store.getters.productIsInStock
//     }
//   },

  methods: {
    ...mapActions({
      fetchProducts: 'fetchProducts'
    }),

    addProductToCart (product){
      this.$store.dispatch('addProductToCart', product)
    }
  },

  created() {
    this.loading = true
    this.$store.dispatch('fetchProducts')
    .then(()=> this.loading = false)
  }

}
</script>

<style scoped>

</style>
