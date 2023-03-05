<template>
  <div id="app">
    <ProductDisplay/>
  </div>
</template>

<script>
import ProductDisplay from './components/Product.vue';

export default {
  name: 'App',
  components: {
    ProductDisplay
  }
}
</script>

<style>
/* css */
body {
  margin: 0;
}
</style>