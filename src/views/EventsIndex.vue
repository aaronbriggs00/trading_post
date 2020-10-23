<template>
  <div class="events-index">
    <div v-for="event in events">
      <h1>{{ event.name }}</h1>
      <router-link :to="`/events/${event.id}`"
        ><img
          src="https://richmondmom.com/wp-content/uploads/2019/04/2019-Farmers-Market-.jpg"
      /></router-link>
      <p>{{ event.city }},{{ event.state }}</p>
      <p>{{ event.date }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      events: [],
    };
  },
  created: function() {
    axios.get("/api/events").then((response) => {
      console.log(response.data);
      this.events = response.data;
    });
  },
  methods: {},
};
</script>
