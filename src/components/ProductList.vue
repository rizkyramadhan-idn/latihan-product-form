<template>
  <div>
    <h4>Product List</h4>

    <p v-if="!productList.length">There is no product in this list.</p>

    <ul v-for="(product, index) in productList" :key="index">
      <li v-on:click="removeProduct(product.id)">{{ product.title }} - Rp. {{ product.price }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    productList: {
      type: Array,
      require: true,
    },
    removeProduct: {
      type: Function,
      require: true,
    },
  },
};
</script>