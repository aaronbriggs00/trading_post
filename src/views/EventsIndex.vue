<template>
  <div class="events-index">
    Search box: <input type="text" v-model="query" />
    <div v-for="event in filterBy(events, query, 'name')">
      <h1>{{ event.name }}</h1>
      <router-link :to="`/events/${event.id}`"
        ><img :src="event.image_url" width="400" height="300"
      /></router-link>
      <p>{{ event.city }},{{ event.state }}</p>
      <p>{{ event.date }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      events: [],
      query: null,
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
