<template>
  <div class="events-show">
    <button
      v-if="!event.current_user_attending && $parent.isLoggedIn()"
      v-on:click="rsvp()"
    >
      let's a go
    </button>
    <button
      v-if="event.current_user_attending && $parent.isLoggedIn()"
      v-on:click="rsvp()"
    >
      let's a not go
    </button>
    <h1>{{ event.name }}</h1>
    <h2>Attendees:</h2>
    <div v-for="user in event.users">
      <router-link :to="`/users/${user.id}`">{{ user.company }}</router-link>
      <h3>Products:</h3>
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
      </div>
      <p>---------------------</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      event: {},
    };
  },
  created: function() {
    axios.get(`/api/events/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.event = response.data;
    });
  },
  methods: {
    rsvp: function() {
      var params = { event_id: this.$route.params.id };
      if (!this.event.current_user_attending) {
        axios.post(`/api/event_users`, params).then((response) => {
          console.log(response.data);
          this.event.current_user_attending = true;
        });
      } else {
        console.log("attempting to delete");
        axios
          .delete(`/api/event_users/${this.$route.params.id}`)
          .then((response) => {
            console.log(response.data);
            this.event.current_user_attending = false;
          });
      }
    },
  },
};
</script>
