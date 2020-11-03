<template>
  <div class="events-index">
    Date:
    <datepicker :clear-button="true" v-model="date"></datepicker><br />
    Search box: <input type="text" v-model="title" />
    <button v-on:click="queryAssign()" class="btn btn-primary">filter</button>
    <p>the selected date is {{ dateQuery }}</p>
    <div
      v-for="event in filterBy(
        filterBy(events, titleQuery, 'name'),
        dateQuery,
        'date'
      )"
    >
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
import Datepicker from "vuejs-datepicker";
import moment from "moment";

export default {
  mixins: [Vue2Filters.mixin],
  components: {
    Datepicker,
  },
  data: function() {
    return {
      events: [],
      title: null,
      date: null,
      titleQuery: null,
      dateQuery: null,
    };
  },
  created: function() {
    axios.get("/api/events").then((response) => {
      console.log(response.data);
      this.events = response.data;
    });
  },
  methods: {
    queryAssign: function() {
      if (this.date) {
        this.dateQuery = this.date.toISOString().split("T")[0];
      } else {
        this.dateQuery = null;
      }
      this.titleQuery = this.title;
    },
  },
};
</script>
