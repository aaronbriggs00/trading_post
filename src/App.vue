<template>
  <div id="app">
    <!-- Navbar -->
    <header>
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container">
          <a class="navbar-brand text-success logo"
            ><i class="mdi mdi-home-map-marker"></i>
            <strong>Trading</strong> Post</a
          >
          <span class="navbar-toggler-icon"></span>
          <div class="collapse navbar-collapse" id="navbarResponsive">
            <ul class="navbar-nav mr-auto mt-2 mt-lg-0 margin-auto">
              <li class="nav-item dropdown">
                <!-- <router-link
                  class="nav-link"
                  to="/home"
                  id="navbarDropdownPortfolio"
                  data-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                >
                  HOME
                </router-link> -->
                <!-- <div
                  class="dropdown-menu"
                  aria-labelledby="navbarDropdownPortfolio"
                >
                  <a class="dropdown-item" href="index1.html"
                    >Home With Search</a
                  >
                  <a class="dropdown-item" href="index2.html">Home With Map</a>
                  <a class="dropdown-item" href="index3.html"
                    >Home With Property Info</a
                  >
                </div> -->
              </li>
              <li class="nav-item dropdown">
                <router-link
                  class="nav-link"
                  to="/about"
                  id="navbarDropdownPortfolio"
                  data-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                >
                  About
                </router-link>
                <!-- <div
                  class="dropdown-menu"
                  aria-labelledby="navbarDropdownPortfolio"
                >
                  <a class="dropdown-item" href="properties-grid.html"
                    >Properties Grid</a
                  >
                  <a class="dropdown-item" href="properties-list.html"
                    >Properties List</a
                  >
                  <a class="dropdown-item" href="property-single-slider.html"
                    >Property Single Slider</a
                  >
                  <a class="dropdown-item" href="property-single-gallery.html"
                    >Property Single Gallery</a
                  >
                </div> -->
              </li>
              <!-- <li class="nav-item dropdown">
                <a
                  class="nav-link dropdown-toggle"
                  href="#"
                  id="navbarDropdownPortfolio"
                  data-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                >
                  Agency
                </a>
                <div
                  class="dropdown-menu"
                  aria-labelledby="navbarDropdownPortfolio"
                >
                  <a class="dropdown-item" href="agency-list.html"
                    >Agency List</a
                  >
                  <a class="dropdown-item" href="agency-profile.html"
                    >Agency Profile</a
                  >
                  <a class="dropdown-item" href="agents.html">Agents</a>
                  <a class="dropdown-item" href="agent-profile.html"
                    >Agent Profile</a
                  >
                </div> -->
              </li>
              <li class="nav-item dropdown">
                <router-link
                  class="nav-link"
                  to="/events"
                  id="navbarDropdownPortfolio"
                  data-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                >
                  Markets
                </router-link>
                <!-- <div
                  class="dropdown-menu"
                  aria-labelledby="navbarDropdownPortfolio"
                >
                  <a class="dropdown-item" href="blog.html">Blog</a>
                  <a class="dropdown-item" href="blog-single.html"
                    >Blog Single</a
                  >
                </div> -->
              </li>
              <li class="nav-item dropdown">
                <a v-if="isLoggedIn()"
                  class="nav-link dropdown-toggle"
                  href="#"
                  id="navbarDropdownPortfolio"
                  data-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                >
                  My Account
                </a>
                <div
                  class="dropdown-menu"
                  aria-labelledby="navbarDropdownPortfolio"
                >
                  <router-link
                    v-if="isLoggedIn()"
                    class="dropdown-item"
                    :to="`/users/${getUserId()}`"
                    >User Profile</router-link
                  >
                  <router-link
                  v-if="isLoggedIn()"
                    class="dropdown-item"
                    :to="`/users/${getUserId()}/edit`"
                    >Edit Profile</router-link
                  >
                  <router-link class="dropdown-item" to="/products/new" v-if="isLoggedIn()"
                    >Add Product</router-link
                  >
                </div>
              </li>
              <!-- <li class="nav-item dropdown">
                <a
                  class="nav-link dropdown-toggle"
                  href="#"
                  id="navbarDropdownPortfolio"
                  data-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                >
                  Pages
                </a>
                <div
                  class="dropdown-menu"
                  aria-labelledby="navbarDropdownPortfolio"
                >
                  <a class="dropdown-item" href="about.html">About Us</a>
                  <a class="dropdown-item" href="faq.html">FAQ</a>
                  <a class="dropdown-item" href="contact.html">Contact</a>
                  <a class="dropdown-item" href="not-found.html">404 Page</a>
                </div>
              </li> -->
            </ul>
            <div class="my-2 my-lg-0">
              <ul class="list-inline main-nav-right">
                <li class="list-inline-item">
                  <router-link v-if="!isLoggedIn()" class="btn btn-link btn-sm" to="/login">Sign in</router-link>
                </li>
                <li class="list-inline-item">
                  <router-link v-if="!isLoggedIn()" class="btn btn-success btn-sm" to="/signup"
                    >Sign Up</router-link
                  >
                </li>
                <li class="list-inline-item">
                  <router-link v-if="isLoggedIn()" class="btn btn-link btn-sm" to="/logout"
                    >Log out</router-link
                  >
                </li>
              </ul>
            </div>
          </div>
        </div>
      </nav>
    </header>
    <router-view :key="$route.path" />
    <!-- Footer -->
    <section class="section-padding bg-dark text-center">
      <h2 class="text-white mt-0">
        I'm happy you're here!
      </h2>
      <p class="text-white mb-4">
        If you're interested in this site or others like it, reach out to me!
      </p>
      <a
        type="button"
        class="btn btn-success"
        href="https://aaronbriggs00.github.io/"
      >
        About me
      </a>
      <router-link
        tag="button"
        type="button"
        class="btn btn-outline-success"
        to="/about"
        >Read More</router-link
      >
    </section>
    <section class="section-padding footer bg-white">
      <div class="container">
        <div class="row">
          <div class="col-lg-4 col-md-3">
            <h4 class="mb-5">
              <a class="text-success logo" href="index.html"
                ><i class="mdi mdi-home-map-marker"></i>
                <strong>Trading</strong>Post</a
              >
            </h4>
            <p>1060 West Addison St, Chicago, Illinois<br />USA 60613</p>
            <p class="mb-0">
              <a class="text-dark" href="#">+1 111 111 1111</a>
            </p>
            <p class="mb-0">
              <a class="text-success" href="#">tradingpost@gmail.com</a>
            </p>
          </div>
          <div class="col-lg-2 col-md-2">
            <h6 class="mb-4">COMPANY</h6>
            <ul>
              <li><a href="#">About us</a></li>
              <li><a href="#">Career</a></li>
              <li><a href="#">Services</a></li>
              <li><a href="#">Properties</a></li>
              <li><a href="#">Contact</a></li>
            </ul>
          </div>
          <div class="col-lg-2 col-md-2">
            <h6 class="mb-4">LEARN MORE</h6>
            <ul>
              <li><a href="#">Privacy</a></li>
              <li><a href="#">Terms & Conditions</a></li>
              <li><a href="#">Account</a></li>
              <li><a href="#">FAQ</a></li>
              <li><a href="#">Blog</a></li>
            </ul>
          </div>
          <div class="col-lg-4 col-md-4">
            <h6 class="mb-4">NEWSLETTER</h6>
            <div class="input-group">
              <input
                type="text"
                class="form-control"
                placeholder="Email Address..."
                aria-label="Recipient's username"
                aria-describedby="basic-addon2"
              />
              <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="button">
                  <i class="mdi mdi-arrow-right"></i>
                </button>
              </div>
            </div>
            <h6 class="mb-4 mt-5">GET IN TOUCH</h6>
            <div class="footer-social">
              <a href="#"><i class="mdi mdi-facebook"></i></a>
              <a href="#"><i class="mdi mdi-twitter"></i></a>
              <a href="#"><i class="mdi mdi-instagram"></i></a>
              <a href="#"><i class="mdi mdi-google"></i></a>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- End Footer -->
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
    };
  },
  created: function() {},
  methods: {
    isLoggedIn: function() {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function() {
      return parseInt(localStorage.getItem("user_id"));
    },
    priceStringCorrect: function(float) {
      if (float) {
        var result = float.toString();
        if (result.endsWith("0")) {
          result += "0";
        }
        return result;
      }
    }
  },
};
</script>
