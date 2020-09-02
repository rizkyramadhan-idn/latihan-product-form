<template>
  <div id="app">
    <div>
      <button v-on:click="toggleUserInfo">{{ showUserInfo ? "Show" : "Hide" }} user details</button>
      <p v-if="showUserInfo">You're logged in!</p>
    </div>

    <br />

    <ProductForm v-bind:addNewProduct="addNewProduct" />

    <br />

    <ProductList v-bind:productList="productList" v-bind:removeProduct="removeProduct" />
  </div>
</template>

<script>
import { ref } from "vue";

import ProductForm from "@/components/ProductForm.vue";
import ProductList from "@/components/ProductList.vue";

export default {
  name: "App",
  setup() {
    const productList = ref([
      { id: Math.random(), title: "test", price: 100000 },
    ]);
    const showUserInfo = ref(false);

    const toggleUserInfo = () => (showUserInfo.value = !showUserInfo.value);

    const addNewProduct = (title, price) =>
      productList.value.push({
        id: Math.random(),
        title,
        price,
      });

    const removeProduct = (productId) => {
      const filteredProductList = productList.value.filter(
        (product) => product.id !== productId
      );

      productList.value = filteredProductList;
    };

    return {
      productList,
      showUserInfo,
      toggleUserInfo,
      addNewProduct,
      removeProduct,
    };
  },
  components: {
    ProductForm,
    ProductList,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
