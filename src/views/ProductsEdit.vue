<template>
  <div class="products-edit">
    {{ product }}
    <input type="text" v-model="product.title" />
    <input type="text" v-model="product.title" />
    <input type="text" v-model="product.title" />
    <input type="text" v-model="product.title" />
    <input type="text" v-model="product.title" />
    <input type="text" v-model="product.title" />
    <input type="text" v-model="product.title" />
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      product: {},
    };
  },
  created: function() {
    axios.get(`/api/products/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.product = response.data;
    });
  },
  methods: {},
};
</script>
