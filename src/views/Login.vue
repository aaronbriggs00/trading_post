<template>
  <div class="login">
    <section class="section-padding">
      <div class="container">
        <div class="row">
          <div class="col-lg-5 col-md-5 mx-auto">
            <div class="card padding-card">
              <div class="card-body">
                <h5 class="card-title mb-4">Login</h5>
                <h6 class="text-danger" v-if="errors">{{ errors[0] }}</h6>
                <form v-on:submit.prevent="submit()">
                  <div class="form-group">
                    <label
                      >Email Address <span class="text-danger"></span
                    ></label>
                    <input
                      v-model="email"
                      type="email"
                      class="form-control"
                      placeholder="Enter Email Address"
                    />
                  </div>
                  <div class="form-group">
                    <label>Password <span class="text-danger"></span></label>
                    <input
                      v-model="password"
                      type="password"
                      class="form-control"
                      placeholder="Enter Password"
                    />
                  </div>
                  <button
                    type="submit"
                    class="btn btn-success btn-block"
                    value="Submit"
                  >
                    LOGIN
                  </button>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      email: "",
      password: "",
      errors: null,
    };
  },
  methods: {
    submit: function() {
      var params = {
        email: this.email,
        password: this.password,
      };
      axios
        .post("/api/sessions", params)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] =
            "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          localStorage.setItem("user_id", response.data.user_id);
          this.$router.push("/events");
        })
        .catch((error) => {
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    },
  },
};
</script>
