<template>
  <div class="events-index">
    <section class="osahan-slider">
      <div id="osahanslider" class="carousel slide" data-ride="carousel">
        <ol class="carousel-indicators">
          <li data-target="#osahanslider" data-slide-to="0" class="active"></li>
          <li data-target="#osahanslider" data-slide-to="1"></li>
        </ol>
        <div class="carousel-inner" role="listbox">
          <div
            class="carousel-item active"
            style="background-image: url('img/slider/2.jpeg')"
          >
            <div class="overlay"></div>
          </div>
          <div
            class="carousel-item"
            style="background-image: url('img/slider/apples.jpeg')"
          >
            <div class="overlay"></div>
          </div>
        </div>
        <a
          class="carousel-control-prev"
          href="#osahanslider"
          role="button"
          data-slide="prev"
        >
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="sr-only">Previous</span>
        </a>
        <a
          class="carousel-control-next"
          href="#osahanslider"
          role="button"
          data-slide="next"
        >
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="sr-only">Next</span>
        </a>
      </div>
      <div class="slider-form">
        <div class="container">
          <h1 class="text-center text-white mb-5">
            Look for a market near you!
          </h1>
          <!-- <form> -->
          <div class="row">
            <div class="col-md-1"></div>
            <div class="col-md-5">
              <div class="input-group">
                <div class="input-group-addon"></div>
                <input
                  class="form-control"
                  placeholder="Search for market by name"
                  type="text"
                  v-model="title"
                />
              </div>
            </div>

            <div class="col-md-5">
              <div class="input-group">
                <div class="input-group-addon">
                  <i class="mdi mdi-google-maps"></i>
                </div>
                <select
                  class="form-control select2 no-radius"
                  v-model="stateQuery"
                >
                  <option value="">Locations</option>
                  <option value="Alabama">Alabama</option>
                  <option value="Alaska">Alaska</option>
                  <option value="Arizona">Arizona</option>
                  <option value="Arkansas">Arkansas</option>
                  <option value="California">California</option>
                  <option value="Colorado">Colorado</option>
                  <option value="Connecticut">Connecticut</option>
                  <option value="Delaware">Delaware</option>
                  <option value="District Of Columbia"
                    >District Of Columbia</option
                  >
                  <option value="Florida">Florida</option>
                  <option value="Georgia">Georgia</option>
                  <option value="Hawaii">Hawaii</option>
                  <option value="Idaho">Idaho</option>
                  <option value="Illinois">Illinois</option>
                  <option value="Indiana">Indiana</option>
                  <option value="Iowa">Iowa</option>
                  <option value="Kansas">Kansas</option>
                  <option value="Kentucky">Kentucky</option>
                  <option value="Louisiana">Louisiana</option>
                  <option value="Maine">Maine</option>
                  <option value="Maryland">Maryland</option>
                  <option value="Massachusetts">Massachusetts</option>
                  <option value="Michicgan">Michigan</option>
                  <option value="Minnesota">Minnesota</option>
                  <option value="Mississippi">Mississippi</option>
                  <option value="Missouri">Missouri</option>
                  <option value="Montana">Montana</option>
                  <option value="Nebraska">Nebraska</option>
                  <option value="Nevada">Nevada</option>
                  <option value="New Hampshire">New Hampshire</option>
                  <option value="New Jersey">New Jersey</option>
                  <option value="New Mexico">New Mexico</option>
                  <option value="New York">New York</option>
                  <option value="North Carolina">North Carolina</option>
                  <option value="North Dakota">North Dakota</option>
                  <option value="Ohio">Ohio</option>
                  <option value="Oklahoma">Oklahoma</option>
                  <option value="Oregon">Oregon</option>
                  <option value="Pennsylvania">Pennsylvania</option>
                  <option value="Rhode Island">Rhode Island</option>
                  <option value="South Carolina">South Carolina</option>
                  <option value="South Dakota">South Dakota</option>
                  <option value="Tennessee">Tennessee</option>
                  <option value="Texas">Texas</option>
                  <option value="Utah">Utah</option>
                  <option value="Vermont">Vermont</option>
                  <option value="Virginia">Virginia</option>
                  <option value="Washington">Washington</option>
                  <option value="West Virginia">West Virginia</option>
                  <option value="Wisconsin">Wisconsin</option>
                  <option value="Wyoming">Wyoming</option>
                </select>
              </div>
            </div>
          </div>
          <!-- </form> -->
        </div>
      </div>
    </section>
    <section class="section-padding">
      <div class="container">
        <div class="row">
          <div class="col-lg-4 col-md-4">
            <div class="card sidebar-card">
              <div class="card-body">
                <h5 class="card-title mb-3">Market By City</h5>
                <ul class="sidebar-card-list">
                  <li>
                    <a v-on:click="cityFilter('newYork')"
                      ><i class="mdi mdi-chevron-right"></i> New York
                      <span class="sidebar-badge">{{
                        newYorkEvents.length
                      }}</span></a
                    >
                  </li>
                  <li>
                    <a v-on:click="cityFilter('sanFrancisco')"
                      ><i class="mdi mdi-chevron-right"></i> San Francisco
                      <span class="sidebar-badge">{{
                        sanFranciscoEvents.length
                      }}</span></a
                    >
                  </li>
                  <li>
                    <a v-on:click="cityFilter('chicago')"
                      ><i class="mdi mdi-chevron-right"></i> Chicago
                      <span class="sidebar-badge">{{
                        chicagoEvents.length
                      }}</span></a
                    >
                  </li>
                  <li>
                    <a v-on:click="cityFilter('houston')"
                      ><i class="mdi mdi-chevron-right"></i> Houston
                      <span class="sidebar-badge">{{
                        houstonEvents.length
                      }}</span></a
                    >
                  </li>
                  <li>
                    <a v-on:click="cityFilter('philadelphia')"
                      ><i class="mdi mdi-chevron-right"></i> Philadelphia
                      <span class="sidebar-badge">{{
                        philadephiaEvents.length
                      }}</span></a
                    >
                  </li>
                  <li>
                    <a v-on:click="cityFilter('boston')"
                      ><i class="mdi mdi-chevron-right"></i> Boston
                      <span class="sidebar-badge">{{
                        bostonEvents.length
                      }}</span></a
                    >
                  </li>
                  <li>
                    <a v-on:click="events = eventsStored"
                      ><i class="mdi mdi-chevron-right"></i> Show all
                      <span class="sidebar-badge">
                        {{ eventsStored.length }}</span
                      ></a
                    >
                  </li>
                </ul>
              </div>
            </div>
            <div class="card sidebar-card">
              <div class="card-body">
                <h5 class="card-title mb-4">Featured Markets</h5>
                <div
                  id="featured-properties"
                  class="carousel slide"
                  data-ride="carousel"
                >
                  <ol class="carousel-indicators">
                    <li
                      data-target="#featured-properties"
                      data-slide-to="0"
                      class="active"
                    ></li>
                    <li
                      data-target="#featured-properties"
                      data-slide-to="1"
                    ></li>
                  </ol>
                  <div class="carousel-inner">
                    <div class="carousel-item active">
                      <div class="card card-list" v-if="featuredEvent1">
                        <router-link :to="`/events/${featuredEvent1.id}`">
                          <img
                            class="card-img-top"
                            :src="featuredEvent1.image_url"
                            alt="Card image cap"
                          />
                          <div class="card-body">
                            <h5 class="card-title">
                              {{ featuredEvent1.name }}
                            </h5>
                            <h6 class="card-subtitle mb-2 text-muted">
                              <i class="mdi mdi-home-map-marker"></i>
                              {{ featuredEvent1.address }}
                            </h6>
                            <h2 class="text-success mb-0 mt-3">
                              <small>{{ featuredEvent1.date }}</small>
                            </h2>
                          </div>
                        </router-link>
                      </div>
                    </div>
                    <div class="carousel-item">
                      <div class="card card-list" v-if="featuredEvent2">
                        <router-link :to="`/events/${featuredEvent2.id}`">
                          <img
                            class="card-img-top"
                            :src="featuredEvent2.image_url"
                            alt="Card image cap"
                          />
                          <div class="card-body">
                            <h5 class="card-title">
                              {{ featuredEvent2.name }}
                            </h5>
                            <h6 class="card-subtitle mb-2 text-muted">
                              <i class="mdi mdi-home-map-marker"></i>
                              {{ featuredEvent2.address }}
                            </h6>
                            <h2 class="text-success mb-0 mt-3">
                              <small>{{ featuredEvent2.date }}}</small>
                            </h2>
                          </div>
                        </router-link>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-8 col-md-8">
            <div class="osahan_top_filter row">
              <div class="col-lg-6 col-md-6 tags-action">
                <p>select date:</p>
                <datepicker :clear-button="true" v-model="date"></datepicker>
                <!-- <span
                  >For Rent <a href="#"><i class="mdi mdi-window-close"></i></a
                ></span>
                <span
                  >Plot/Land <a href="#"><i class="mdi mdi-window-close"></i></a
                ></span> -->
              </div>
              <div class="col-lg-6 col-md-6 sort-by-btn float-right">
                <!-- <div class="view-mode float-right">
                  <a href="properties-grid.html"><i class="mdi mdi-grid"></i></a
                  ><a class="active" href="properties-list.html"
                    ><i class="mdi mdi-format-list-bulleted"></i
                  ></a>
                </div> -->
                <div class="dropdown float-right">
                  <button
                    class="btn btn-success btn-sm dropdown-toggle"
                    type="button"
                    id="dropdownMenuButton"
                    data-toggle="dropdown"
                    aria-haspopup="true"
                    aria-expanded="false"
                  >
                    <i class="mdi mdi-filter"></i> {{ queryOption }}
                  </button>
                  <div
                    class="dropdown-menu float-right"
                    aria-labelledby="dropdownMenuButton"
                  >
                    <a
                      class="dropdown-item"
                      v-on:click="querySelect('Popularity')"
                      ><i class="mdi mdi-chevron-right"></i> Popularity
                    </a>
                    <a class="dropdown-item" v-on:click="querySelect('New')"
                      ><i class="mdi mdi-chevron-right"></i> New
                    </a>
                  </div>
                </div>
              </div>
            </div>
            <div class="row">
              <div class="col-lg-12 col-md-12">
                <div
                  class="card card-list card-list-view"
                  v-for="event in filterBy(
                    filterBy(
                      filterBy(events, title, 'name'),
                      formattedDate,
                      'date'
                    ),
                    stateQuery,
                    'address'
                  ).slice((paginationNumber - 1) * 10, paginationNumber * 10)"
                >
                  <router-link :to="`/events/${event.id}`">
                    <div class="row no-gutters">
                      <div class="col-lg-5 col-md-5">
                        <img
                          class="card-img-top"
                          :src="event.image_url"
                          alt="Card image cap"
                        />
                      </div>
                      <div class="col-lg-7 col-md-7">
                        <div class="card-body">
                          <h5 class="card-title">{{ event.name }}</h5>
                          <h6 class="card-subtitle mb-2 text-muted">
                            <i class="mdi mdi-home-map-marker"></i>
                            {{ event.address }}
                          </h6>
                          <h2 class="text-success mb-0 mt-3">
                            <small>{{ event.date }}</small>
                          </h2>
                        </div>
                        <div class="card-footer">
                          <span
                            ><i class="mdi mdi-sofa"></i> Vendors :
                            <strong>{{ event.users }}</strong></span
                          >
                        </div>
                      </div>
                    </div>
                  </router-link>
                </div>
              </div>
            </div>
            <nav class="mt-5">
              <ul class="pagination justify-content-center">
                <li class="page-item">
                  <a
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + -1)"
                    v-if="paginationNumber > 1"
                  >
                    <i class="mdi mdi-chevron-left"></i>
                  </a>
                </li>
                <li class="page-item active">
                  <button
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber)"
                  >
                    {{ paginationNumber }}
                  </button>
                </li>
                <li class="page-item">
                  <button
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 1)"
                  >
                    {{ paginationNumber + 1 }}
                  </button>
                </li>
                <li class="page-item">
                  <button
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 2)"
                  >
                    {{ paginationNumber + 2 }}
                  </button>
                </li>
                <li class="page-item">
                  <button
                    v-if="paginationShowMore == false"
                    class="page-link"
                    v-on:click="paginationShowMore = true"
                  >
                    ...
                  </button>
                </li>
                <li class="page-item">
                  <button
                    v-if="paginationShowMore"
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 3)"
                  >
                    {{ paginationNumber + 3 }}
                  </button>
                </li>
                <li class="page-item">
                  <button
                    v-if="paginationShowMore"
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 4)"
                  >
                    {{ paginationNumber + 4 }}
                  </button>
                </li>
                <li class="page-item">
                  <button
                    v-if="paginationShowMore"
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 5)"
                  >
                    {{ paginationNumber + 5 }}
                  </button>
                </li>
                <li class="page-item">
                  <button
                    v-if="paginationShowMore"
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 6)"
                  >
                    {{ paginationNumber + 6 }}
                  </button>
                </li>
                <li class="page-item">
                  <button
                    v-if="paginationShowMore"
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 7)"
                  >
                    {{ paginationNumber + 7 }}
                  </button>
                </li>
                <li class="page-item">
                  <button
                    v-if="paginationShowMore"
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 8)"
                  >
                    {{ paginationNumber + 8 }}
                  </button>
                </li>
                <li class="page-item">
                  <button
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 9)"
                  >
                    {{ paginationNumber + 9 }}
                  </button>
                </li>
                <li class="page-item">
                  <a
                    class="page-link"
                    v-on:click="paginationGo(paginationNumber + 1)"
                  >
                    <i class="mdi mdi-chevron-right"></i>
                  </a>
                </li>
              </ul>
            </nav>
          </div>
        </div>
      </div>
    </section>
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
      stateQuery: "",
      paginationNumber: 1,
      paginationShowMore: false,
      queryOption: "sort by",
      featuredEvent1: null,
      featuredEvent2: null,
      chicagoEvents: [],
      bostonEvents: [],
      newYorkEvents: [],
      sanFranciscoEvents: [],
      philadephiaEvents: [],
      houstonEvents: [],
      eventsStored: [],
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
    axios.get("/api/events?current=yes").then((response) => {
      console.log(response.data);
      this.events = response.data;
      this.featuredEvent1 = response.data[7];
      this.featuredEvent2 = response.data[14];
      this.chicagoEvents = response.data.filter((event) =>
        event.address.includes("Chicago")
      );
      this.newYorkEvents = response.data.filter((event) =>
        event.address.includes("New York")
      );
      this.houstonEvents = response.data.filter((event) =>
        event.address.includes("Houston")
      );
      this.bostonEvents = response.data.filter((event) =>
        event.address.includes("Boston")
      );
      this.philadelphiaEvents = response.data.filter((event) =>
        event.address.includes("Philadelphia")
      );
      this.sanFranciscoEvents = response.data.filter((event) =>
        event.address.includes("San Francisco")
      );
      this.eventsStored = this.events;
    });
  },
  methods: {
    paginationGo: function(page) {
      console.log(page);
      this.paginationNumber = page;
    },
    cityFilter: function(city) {
      if (city === "newYork") {
        this.events = this.newYorkEvents;
      } else if (city === "sanFrancisco") {
        this.events = this.sanFranciscoEvents;
      } else if (city === "chicago") {
        this.events = this.chicagoEvents;
      } else if (city === "houston") {
        this.events = this.houstonEvents;
      } else if (city === "philadelphia") {
        this.events = this.philadelphiaEvents;
      } else if (city === "boston") {
        this.events = this.bostonEvents;
      }
    },
    querySelect: function(option) {
      this.paginationNumber = 1;
      this.queryOption = option;
      if (option == "Popularity") {
        console.log("sorting by users");
        this.events = this.events.sort((a, b) => (a.users > b.users ? -1 : 1));
      } else if (option == "New") {
        console.log("sorting by date");
        this.events = this.events.sort((a, b) => (a.date > b.date ? 1 : -1));
      }
    },
  },
};
</script>
