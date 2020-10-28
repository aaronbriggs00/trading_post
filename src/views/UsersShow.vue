<template>
  <div class="users-show">
    <img :src="user.image_url" alt="" />
    <p>{{ user }}</p>
    <router-link
      v-if="$parent.getUserId() == $route.params.id"
      :to="`/users/${$route.params.id}/edit`"
      tag="button"
    >
      edit profile
    </router-link>
    <h2>Products:</h2>
    <router-link
      v-if="$parent.getUserId() == $route.params.id"
      tag="button"
      to="/products/new"
      >add product</router-link
    >
    <!-- user's products -->
    <div v-for="product in user.products">
      <h3>{{ product.title }} - {{ product.category }}</h3>
      <p v-if="!product.per_unit_pricing">
        ${{ parseFloat(product.price).toFixed(2) }}
      </p>
      <p v-if="product.per_unit_pricing">
        ${{ parseFloat(product.price).toFixed(2) }}/{{ product.unit }}
      </p>
      <img :src="product.image_url" alt="" />
      <p>{{ product.description }}</p>
      <router-link
        v-if="$parent.getUserId() == $route.params.id"
        :to="`/products/${product.id}/edit`"
        tag="button"
      >
        edit product
      </router-link>
    </div>
    <h2>Schedule:</h2>
    <!-- user's events -->
    <div v-for="event in user.events">
      {{ event }}
      <router-link tag="button" :to="`/events/${event.id}`">view</router-link>
    </div>

    <!-- <router-link to="" tag="button">add product</router-link> -->
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      user: {},
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
    });
  },
  methods: {},
};
</script>
