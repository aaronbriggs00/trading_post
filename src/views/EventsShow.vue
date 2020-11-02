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
    <img :src="event.image_url" width="400" height="300" />
    <h3>{{ event.address }}</h3>
    <div id="map"></div>
    <h2>Attendees:</h2>
    <div v-for="user in event.users">
      <router-link :to="`/users/${user.id}`">{{ user.company }}</router-link
      ><br />
      <img :src="user.image_url" alt="" />
      <h3>Products:</h3>
      <div v-for="product in user.products">
        <h3>{{ product.title }} - {{ product.category }}</h3>
        <p v-if="!product.per_unit_pricing">
          ${{ parseFloat(product.price).toFixed(2) }}
        </p>
        <p v-if="product.per_unit_pricing">
          ${{ parseFloat(product.price).toFixed(2) }}/{{ product.unit }}
        </p>
        <img :src="product.image_url" alt="" width="400" height="300" />
        <p>{{ product.description }}</p>
      </div>
      <p>---------------------</p>
    </div>
  </div>
</template>

<style>
#map {
  position: absolute;
  height: 300px;
  width: 100%;
}
</style>

<script>
import axios from "axios";
import mapboxgl from "mapbox-gl";

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
      console.log(this.event.address);
      mapboxgl.accessToken = process.env.VUE_APP_MAP_BOX_API_KEY;
      var mapboxClient = mapboxSdk({ accessToken: mapboxgl.accessToken });
      mapboxClient.geocoding
        .forwardGeocode({
          query: this.event.address,
          autocomplete: false,
          limit: 1,
        })
        .send()
        .then(function(response) {
          if (
            response &&
            response.body &&
            response.body.features &&
            response.body.features.length
          ) {
            var feature = response.body.features[0];
            var map = new mapboxgl.Map({
              container: "map",
              style: "mapbox://styles/mapbox/streets-v11",
              center: feature.center,
              zoom: 10,
            });
            new mapboxgl.Marker().setLngLat(feature.center).addTo(map);
          }
        });
    });
  },
  mounted: function() {
    // this.mapAddress();
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
    mapAddress: function() {
      console.log(this.event.address);
      mapboxgl.accessToken =
        "pk.eyJ1IjoiYWFyb25icmlnZ3MwMCIsImEiOiJja2dxcnhnenowamRkMnNyM2dxamJucGFnIn0.-bUuU_osNL1i7Ajwgo0sew";
      var mapboxClient = mapboxSdk({ accessToken: mapboxgl.accessToken });
      mapboxClient.geocoding
        .forwardGeocode({
          query: this.event.address,
          autocomplete: false,
          limit: 1,
        })
        .send()
        .then(function(response) {
          if (
            response &&
            response.body &&
            response.body.features &&
            response.body.features.length
          ) {
            var feature = response.body.features[0];
            var map = new mapboxgl.Map({
              container: "map",
              style: "mapbox://styles/mapbox/streets-v11",
              center: feature.center,
              zoom: 10,
            });
          }
        });
    },
  },
};
</script>
