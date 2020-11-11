<template>
  <div class="events-show">
    <h1>{{ event.users.map((user) => user.id) }}</h1>
    <button
      v-if="!event.current_user_attending && $parent.isLoggedIn()"
      v-on:click="rsvp()"
    >
      let's a go
    </button>
    <button
      v-if="event.current_user_attending && $parent.isLoggedIn()"
      v-on:click="
        rsvp();
        categoryData();
      "
    >
      let's a not go
    </button>
    <button
      v-on:click="
        toggleAnalytics();
        categoryData();
      "
    >
      Show Graphs
    </button>
    <div v-if="showGraph">
      <doughnut-chart
        :chartData="categoryChartData"
        :options="categoryChartOptions"
      ></doughnut-chart>
    </div>
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
import DoughnutChart from "./../components/DoughnutChart.js";

export default {
  components: {
    DoughnutChart,
  },
  data: function() {
    return {
      event: {},
      currentUserData: {},
      showGraph: false,
      categoryChartData: null,
      categoryChartOptions: {},
    };
  },
  created: function() {
    axios.get(`/api/events/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.event = response.data;
      console.log(this.event.address);
      // mapboxgl.accessToken = process.env.VUE_APP_MAP_BOX_API_KEY;
      // var mapboxClient = mapboxSdk({ accessToken: mapboxgl.accessToken });
      // mapboxClient.geocoding
      //   .forwardGeocode({
      //     query: this.event.address,
      //     autocomplete: false,
      //     limit: 1,
      //   })
      //   .send()
      //   .then(function(response) {
      //     if (
      //       response &&
      //       response.body &&
      //       response.body.features &&
      //       response.body.features.length
      //     ) {
      //       var feature = response.body.features[0];
      //       var map = new mapboxgl.Map({
      //         container: "map",
      //         style: "mapbox://styles/mapbox/streets-v11",
      //         center: feature.center,
      //         zoom: 10,
      //       });
      //       new mapboxgl.Marker().setLngLat(feature.center).addTo(map);
      //     }
      //   });
    });
    axios.get(`/api/users/${this.$parent.getUserId()}`).then((response) => {
      console.log(response.data);
      this.currentUserData = response.data;
    });
  },
  mounted: function() {
    // this.mapAddress();
  },
  computed: {},
  methods: {
    rsvp: function() {
      var params = { event_id: this.$route.params.id };
      if (!this.event.current_user_attending) {
        axios.post(`/api/event_users`, params).then((response) => {
          console.log(response.data);
          this.event.users.splice(0, 0, this.currentUserData);
          this.event.current_user_attending = true;
        });
      } else {
        console.log("attempting to delete");
        axios
          .delete(`/api/event_users/${this.$route.params.id}`)
          .then((response) => {
            console.log(response.data);
            this.event.current_user_attending = false;
            this.event.users = this.event.users.filter(
              (user) => user.id != this.$parent.getUserId()
            );
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
    toggleAnalytics: function() {
      if (this.showGraph) {
        this.showGraph = false;
      } else {
        this.showGraph = true;
      }
    },
    categoryData: function() {
      var categoriesHash = {};
      this.event.users.forEach((user) => {
        user.products.forEach((product) => {
          if (categoriesHash[product.category]) {
            categoriesHash[product.category] += 1;
          } else {
            categoriesHash[product.category] = 1;
          }
        });
      });
      var categoryData = [];
      Object.keys(categoriesHash).forEach((key) => {
        categoryData.push(categoriesHash[key]);
      });
      this.categoryChartData = {
        datasets: [
          {
            data: categoryData,
            backgroundColor: [
              "#9999ff",
              "#ff6666",
              "#196666",
              "#00cc99",
              "#6600cc",
              "#ffd966",
              "#c2d6d6",
              "#ffcccc",
              "#ffe6ff",
              "#808000",
              "#004d66",
              "#d9d9d9",
              "#a9ff4d",
              "#66ffff",
              "#ffc266",
              "e6f8ff",
              "#4080bf",
              "#cc6699",
              "#4d001f",
              "#333399",
              "#73264d",
              "#cccc00",
              "#ff0066",
              "#206040",
              "#86b300",
              "#394d00",
              "#ccccff",
              "#ffcc99",
              "#ac3973",
            ],
          },
        ],
        labels: Object.keys(categoriesHash),
      };
    },
  },
};
</script>
