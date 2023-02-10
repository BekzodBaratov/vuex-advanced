<template>
  <ul>
    <li v-for="product in products" :key="product.id">
      {{ product.title }} - {{ currency(product.price) }}
      <br />
      <button :disabled="!product.inventory" @click="addProductToCart(product)">
        Add to cart
      </button>
    </li>
  </ul>
</template>

<script setup>
import { computed } from "vue";
import { useStore } from "vuex";
import { currency } from "../../currency";
const store = useStore();

const products = computed(() => store.state.products.all);

const addProductToCart = (product) =>
  store.dispatch("cart/addProductToCart", product);
store.dispatch("products/getAllProducts");

// computed: mapState({
//   products: state => state.products.all
// }),
// methods: mapActions('cart', [
//   'addProductToCart'
// ]),
// created () {
//   this.$store.dispatch('products/getAllProducts')
// }
</script>
