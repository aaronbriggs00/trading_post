<template>
  <div class="users-show">
    <!-- Inner Header -->
    <section class="section-padding bg-dark inner-header">
      <div class="container">
        <div class="row">
          <div class="col-md-12 text-center">
            <h1 class="mt-0 mb-3 text-white">Vendor</h1>
            <div class="breadcrumbs">
              <p class="mb-0 text-white">
                <router-link class="text-white" to="/events"
                  >Markets</router-link
                >
                /
                <span class="text-success">View Profile</span>
                /
                <router-link
                  class="text-white"
                  v-if="$parent.getUserId() == $route.params.id"
                  :to="`/users/${$route.params.id}/edit`"
                  >Edit Profile</router-link
                >
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- End Inner Header -->
    <!-- Vendor -->
    <section class="section-padding">
      <div class="container">
        <div class="row">
          <div class="col-lg-5 col-md-5">
            <img
              class="rounded img-fluid"
              :src="user.image_url"
              alt="Card image cap"
            />
          </div>
          <div class="col-lg-7 col-md-7 pl-5 pr-5">
            <h1 class="mb-0 mt-4">
              {{ user.company }}
            </h1>
            <h5 class="text-success mb-3">Vendor</h5>
            <p>
              {{ user.bio }}
            </p>
            <div class="row mt-3">
              <div class="col-lg-6 col-md-6">
                <p>
                  <strong class="text-dark">Phone :</strong>
                  {{ user.phone_number }}
                </p>
                <p>
                  <strong class="text-dark">Address :</strong>
                  {{ user.address }}
                </p>
              </div>
              <div class="col-lg-6 col-md-6">
                <p>
                  <strong class="text-dark">Website :</strong>
                  {{ user.website }}
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
        </div>
      </div>
    </section>
    <!-- End Vendor -->
    <!-- My Products -->
    <section class="section-padding  border-top">
      <div class="container">
        <div class="row">
          <div class="col-lg-12 col-md-12 section-title text-left mb-4">
            <div class="row">
              <div class="col-lg-3 col-md-4">
                <h2>Current Products</h2>
              </div>
              <div class="view-mode float-right">
                <router-link
                  v-if="$parent.getUserId() == $route.params.id"
                  id="plus-button"
                  to="/products/new"
                  class="btn btn-outline-secondary"
                  tag="button"
                >
                  add
                </router-link>
              </div>
            </div>
          </div>
          <div class="col-lg-4 col-md-4" v-for="product in user.products">
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
    </section>
    <!-- End My Products -->
    <!-- Schedule -->
    <section class="section-padding bg-white text-center">
      <h2 class="text mt-0">
        Schedule
      </h2>
      <div class="kalendar-view">
        <kalendar
          class="kalendar-widget"
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
            <h5 class="card-title">
              {{ event_information.data.title }}
            </h5>
            <router-link tag="span" :to="`/events/${event_information.data.id}`"
              >view</router-link
            >
          </div>
        </kalendar>
      </div>
    </section>
    <!-- End Schedule -->
    <!-- Contact Me -->
    <section class="section-padding  bg-white">
      <div class="container">
        <div class="row">
          <div class="col-lg-12 col-md-12 section-title text-left mb-4">
            <h2>Contact Me</h2>
          </div>
          <form class="col-lg-12 col-md-12" name="sentMessage">
            <div class="row">
              <div class="control-group form-group col-lg-4 col-md-4">
                <div class="controls">
                  <label>Your Name <span class="text-danger">*</span></label>
                  <input type="text" class="form-control" required />
                </div>
              </div>
              <div class="control-group form-group col-lg-4 col-md-4">
                <div class="controls">
                  <label
                    >Email Address <span class="text-danger">*</span></label
                  >
                  <input type="email" class="form-control" required />
                </div>
              </div>
              <div class="control-group form-group col-lg-4 col-md-4">
                <div class="controls">
                  <label>Phone Number <span class="text-danger">*</span></label>
                  <input type="email" class="form-control" required />
                </div>
              </div>
            </div>
            <div class="control-group form-group">
              <div class="controls">
                <label>Message <span class="text-danger">*</span></label>
                <textarea rows="10" cols="100" class="form-control"></textarea>
              </div>
            </div>
            <button type="submit" class="btn btn-success">Send Message</button>
          </form>
        </div>
      </div>
    </section>
    <!-- End Contact Me -->
  </div>
</template>

<style>
.kalendar-widget {
  padding-bottom: 550px;
  padding-left: 125px;
  padding-right: 125px;
}
.kalendar-view {
  max-height: 750px;
  padding: 100px;
}
</style>

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
        cell_height: 6,
        scrollToNow: false,
        start_day: new Date().toISOString(),
        read_only: true,
        day_starts_at: 8,
        day_ends_at: 20,
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
          from: `${event.date}T15:00:00Z`,
          to: `${event.date}T24:00:00Z`,
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
