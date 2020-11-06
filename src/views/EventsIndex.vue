<template>
  <div class="events-index">
    Date:
    <datepicker :clear-button="true" v-model="date"></datepicker><br />
    Search box: <input type="text" v-model="title" />
    <p>the selected date is {{ formattedDate }}</p>
    <p>the output date looks like {{ date }}</p>
    <div
      v-for="event in filterBy(
        filterBy(events, title, 'name'),
        formattedDate,
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
  computed: {
    formattedDate: function() {
      if (this.date) {
        return this.date.toISOString().split("T")[0];
      } else {
        return null;
      }
    },
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
