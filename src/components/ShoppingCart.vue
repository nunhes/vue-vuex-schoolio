<template>
  <div>
    <h1>Shopping Cart</h1>
    <ul>
      <li v-for="product in products">
         {{product.title}} - {{product.price | currency}} - {{product.inventory}}
      </li>
    </ul>
    <p>Total: {{total | currency}}</p>
    <button @click="$store.dispatch('checkout')">Checkout</button>
    <p v-if="checkoutStatus">{{checkoutStatus}}</p>
  </div>
</template>

<script>
import {mapState, mapGetters} from 'vuex'

export default {
  computed: {
    ...mapGetters({
      products: 'cartProducts',
      total: 'cartTotal'
    }),

    ...mapState({
      checkoutStatus: 'checkoutStatus'
    })
  },
}
</script>

<style scoped>

</style>
