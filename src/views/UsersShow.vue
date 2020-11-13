<template>
  <div class="users-show">
    <h1>{{ events }}</h1>
    <img :src="user.image_url" alt="" />
    <h1>{{ user.first_name }} {{ user.last_name }}</h1>
    <h2>{{ user.company }}</h2>
    <p>{{ user.email }}</p>
    <p>{{ user.bio }}</p>
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
      <h3>{{ event.name }}</h3>
      <p>{{ event.address }}</p>
      <p>{{ event.date }}</p>
      <router-link tag="button" :to="`/events/${event.id}`">view</router-link>
    </div>
    <kalendar
      v-if="events"
      :configuration="calendar_settings"
      :events.sync="events"
    >
      <!-- CREATED CARD SLOT -->
      <div
        slot="created-card"
        slot-scope="{ event_information }"
        class="details-card"
      >
        <h4 class="appointment-title">
          {{ event_information.data.title }}
        </h4>
        <router-link :to="`/events/${event_information.data.id}`"
          >view</router-link
        >
      </div>
    </kalendar>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import { Kalendar } from "kalendar-vue";

export default {
  components: {
    Kalendar,
  },
  data: function() {
    return {
      user: {},
      calendar_settings: {
        style: "material_design",
        view_type: "week",
        cell_height: 2,
        scrollToNow: false,
        start_day: new Date().toISOString(),
        read_only: true,
        day_starts_at: 0,
        day_ends_at: 24,
        overlap: true,
        hide_dates: ["2019-10-31"], // Spooky
        hide_days: [6],
        past_event_creation: true,
      },
      events: null,
    };
  },
  created: function() {
    var formattedEvents = [];
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
      response.data.events.forEach((event) => {
        console.log(event);
        formattedEvents.push({
          from: `${event.date}T12:00:00Z`,
          to: `${event.date}T18:00:00Z`,
          data: {
            title: `${event.name}`,
            description: `${event.address}`,
            id: `${event.id}`,
          },
        });
        console.log(formattedEvents);
      });
      this.events = formattedEvents;
    });
  },
  methods: {},
};
</script>
