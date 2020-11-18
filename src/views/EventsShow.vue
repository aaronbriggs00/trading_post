<template>
  <div class="events-show">
    <!-- Inner Header -->
    <section class="section-padding bg-dark inner-header">
      <div class="container">
        <div class="row">
          <div class="col-md-12 text-center">
            <h1 class="mt-0 mb-3 text-white">{{ event.name }}</h1>
          </div>
        </div>
      </div>
    </section>
    <!-- End Inner Header -->
    <!-- Market Info -->
    <section class="section-padding">
      <div class="container">
        <div class="dropdown float-right">
          <button
            class="btn btn-success btn-sm dropdown-toggle"
            type="button"
            id="dropdownMenuButton"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            <i class="mdi mdi-filter"></i> {{ dropdown }}
          </button>
          <div
            class="dropdown-menu float-right"
            aria-labelledby="dropdownMenuButton"
          >
            <a
              v-if="!showInfo"
              class="dropdown-item"
              v-on:click="
                showMap = false;
                showGraph = false;
                showInfo = true;
                removeMap();
              "
              ><i class="mdi mdi-chevron-right"></i> Information
            </a>
            <a
              v-if="!showGraph"
              class="dropdown-item"
              v-on:click="
                showMap = false;
                showInfo = false;
                showGraph = true;
                removeMap();
                categoryData();
              "
              ><i class="mdi mdi-chevron-right"></i> Market Data
            </a>
            <a
              v-if="!showMap"
              class="dropdown-item"
              v-on:click="
                showInfo = false;
                showGraph = false;
                showMap = true;
                mapAddress();
              "
              ><i class="mdi mdi-chevron-right"></i> Map
            </a>
          </div>
        </div>
        <div id="event-header" class="row">
          <div class="col-lg-5 col-md-5">
            <h1>{{ event.date }}</h1>
            <button
              class="btn btn btn-outline-secondary"
              v-if="!event.current_user_attending && $parent.isLoggedIn()"
              v-on:click="rsvp()"
            >
              Not Attending
            </button>
            <button
              class="btn btn-success btn-sm"
              v-if="event.current_user_attending && $parent.isLoggedIn()"
              v-on:click="
                rsvp();
                categoryData();
              "
            >
              Attending
            </button>
          </div>
        </div>
        <div class="row">
          <div class="col-lg-5 col-md-5">
            <img
              class="rounded img-fluid"
              :src="event.image_url"
              alt="Card image cap"
            />
          </div>
          <div v-if="showInfo" class="col-lg-7 col-md-7 pl-5 pr-5">
            <div class="row mt-3">
              <div class="col-lg-6 col-md-6">
                <p>
                  <strong class="text-dark">Address :</strong>
                  {{ event.address }}
                </p>
                <a :href="event.website"
                  ><strong class="text-dark">Web Link</strong></a
                >
              </div>
              <div class="col-lg-6 col-md-6">
                <p>
                  <strong class="text-dark">Products :</strong>
                  {{ event.products }}
                </p>
              </div>
            </div>
            <div class="footer-social">
              <span>Follow : </span>
              <a href="#"><i class="mdi mdi-facebook"></i></a>
              <a href="#"><i class="mdi mdi-twitter"></i></a>
              <a href="#"><i class="mdi mdi-instagram"></i></a>
              <a href="#"><i class="mdi mdi-google"></i></a>
            </div>
          </div>
          <div v-if="showGraph" class="col-lg-7 col-md-7 pl-5 pr-5">
            <doughnut-chart
              :chartData="categoryChartData"
              :options="categoryChartOptions"
            ></doughnut-chart>
          </div>
          <div class="col-lg-7 col-md-7 pl-5 pr-5">
            <div v-if="showMap" id="map"></div>
          </div>
        </div>
      </div>
    </section>
    <!-- End Market Info -->
    <!-- Users -->
    <section class="section-padding">
      <div class="container">
        <div class="row">
          <h3>Attending</h3>
          <div class="col-lg-12 col-md-12">
            <div class="row" v-for="user in event.users">
              <div class="col-lg-12 col-md-12">
                <div class="card card-list card-list-view">
                  <a :to="`/users/${user.id}`">
                    <div class="row no-gutters">
                      <div class="col-lg-4 col-md-4">
                        <img
                          class="card-img-top"
                          :src="user.image_url"
                          alt="Card image cap"
                        />
                      </div>
                      <div class="col-lg-8 col-md-8">
                        <div class="card-body">
                          <h3>{{ user.company }}</h3>
                          <h6 class="card-subtitle mt-1 mb-4 text-muted">
                            <i class="mdi mdi-home-map-marker"></i>
                            {{ user.address }}
                          </h6>
                          <p class="mb-0">{{ user.bio }}</p>
                          <br />
                          <div>
                            <span
                              class="btn btn-success btn-sm"
                              v-on:click="
                                showProducts = true;
                                productButtonReset(user.id);
                              "
                              >Products</span
                            >
                            <router-link
                              :to="`/users/${user.id}`"
                              class="btn btn-link btn-sm"
                            >
                              Profile
                            </router-link>
                          </div>
                          <br /><br />
                          <div v-for="category in user.categories">
                            <h5 class="card-subtitle mb-2 text-muted">
                              {{ category.title }}
                            </h5>
                          </div>
                        </div>
                        <div class="card-footer">
                          <span
                            ><i class="mdi mdi-phone"></i>
                            {{ user.phone_number }}</span
                          >
                          <span
                            ><i class="mdi mdi-email"></i> {{ user.email }}
                          </span>
                          <span
                            ><i class="mdi mdi-link"></i>
                            {{ user.website }}</span
                          >
                        </div>
                      </div>
                    </div>
                  </a>
                </div>
              </div>
              <div
                v-if="selectedUser == user.id"
                class="col-lg-4 col-md-4"
                v-for="product in user.products"
              >
                <div class="card card-list">
                  <a href="#">
                    <span
                      v-if="product.price_negotiable"
                      class="badge badge-success"
                      >Negotiable</span
                    >
                    <img
                      class="card-img-top"
                      :src="product.image_url"
                      alt="Card image cap"
                    />
                    <div class="card-body">
                      <h5 class="card-title">{{ product.title }}</h5>
                      <h5 class="card-subtitle mb-2 text-muted">
                        {{ product.category }}
                      </h5>
                      <h2 class="text-success mb-0 mt-3">
                        ${{ $parent.priceStringCorrect(product.price) }}
                        <small v-if="product.unit">/{{ product.unit }}</small>
                      </h2>
                      <br />
                      <h6 class="card-subtitle mb-2 text-muted">
                        {{ product.description }}
                      </h6>
                    </div>
                    <div class="card-footer">
                      <router-link
                        v-if="$parent.getUserId() == $route.params.id"
                        :to="`/products/${product.id}/edit`"
                        tag="span"
                        ><i class="mdi mdi-move-resize-variant"></i>
                        edit product
                      </router-link>
                    </div>
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- End Users -->
  </div>
</template>

<style>
#map {
  height: 28em;
  width: 42em;
}
#event-header {
  padding-bottom: 11px;
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
      selectedUser: null,
      showGraph: false,
      showMap: false,
      showInfo: true,
      categoryChartData: null,
      categoryChartOptions: {},
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
              style: "mapbox://styles/mapbox/light-v10",
              center: feature.center,
              zoom: 10,
            });
          }
        });
    });
    axios.get(`/api/users/${this.$parent.getUserId()}`).then((response) => {
      console.log(response.data);
      this.currentUserData = response.data;
    });
  },
  mounted: function() {
    this.mapAddress();
  },
  computed: {
    dropdown: function() {
      if (this.showInfo === true) {
        return "Information";
      } else if (this.showGraph === true) {
        return "Market Data";
      } else {
        return "Map";
      }
    },
  },
  methods: {
    productButtonReset: function(input) {
      if (this.selectedUser) {
        this.selectedUser = null;
      } else {
        this.selectedUser = input;
      }
    },
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
          new mapboxgl.Marker().setLngLat(feature.center).addTo(map);
        });
    },
    removeMap: function() {
      var map = document.getElementById("demo");
      if (map) {
        map.remove();
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
