<template>
  <div>
    <h4>Product Form</h4>

    <form>
      <label for="title">Product Title</label>
      <input v-model="product.title" type="text" placeholder="Enter product title" />

      <label for="title">Product Price</label>
      <input v-model="product.price" type="number" placeholder="Enter product price" />

      <button v-on:click="submitProduct" v-bind:disabled="!isFormValid">Submit</button>
    </form>
  </div>
</template>

<script>
import { reactive, computed, ref, watchEffect } from "vue";

export default {
  props: {
    addNewProduct: {
      type: Function,
      require: true,
    },
  },
  setup(props) {
    const product = reactive({
      title: "",
      price: "",
    });
    const formSubmitted = ref(false);

    const floatPrice = computed(() => parseFloat(product.price));

    const isFormValid = computed(() => {
      if (product.title.trim().length === 0) {
        return false;
      }

      if (isNaN(floatPrice.value) || floatPrice.value <= 0) {
        return false;
      }

      return true;
    });

    const submitProduct = (event) => {
      event.preventDefault();
      console.log(`${product.title} - ${product.price}`);

      props.addNewProduct(product.title, floatPrice.value);

      formSubmitted.value = true;
    };

    watchEffect(() => {
      if (formSubmitted.value) {
        product.title = "";
        product.price = "";

        formSubmitted.value = false;
      }
    });

    return {
      product,
      submitProduct,
      isFormValid,
    };
  },
};
</script>