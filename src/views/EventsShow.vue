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
    <h1>{{ event }}}</h1>
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
  methods: {},
};
</script>
