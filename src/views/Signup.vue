<template>
  <div class="signup">
    <!-- Register -->
    <section class="section-padding">
      <div class="container">
        <div class="row">
          <div class="col-lg-5 col-md-5 mx-auto">
            <div class="card padding-card">
              <div class="card-body">
                <h5 class="card-title mb-4">Register</h5>
                <h6 v-if="errors">{{ errors }}</h6>
                <form v-on:submit.prevent="submit()">
                  <div class="form-group">
                    <label>Company <span class="text-danger">*</span></label>
                    <input
                      v-model="company"
                      type="text"
                      class="form-control"
                      placeholder="Enter Company Name"
                    />
                  </div>
                  <div class="form-group">
                    <label
                      >Email Address <span class="text-danger">*</span></label
                    >
                    <input
                      v-model="email"
                      type="email"
                      class="form-control"
                      placeholder="Enter Email Address"
                    />
                  </div>
                  <div class="form-group">
                    <label>Password <span class="text-danger">*</span></label>
                    <input
                      v-model="password"
                      type="password"
                      class="form-control"
                      placeholder="Enter Password"
                    />
                  </div>
                  <div class="form-group">
                    <label
                      >Password Confirmation
                      <span class="text-danger">*</span></label
                    >
                    <input
                      v-model="passwordConfirmation"
                      type="password"
                      class="form-control"
                      placeholder="Re-type Password"
                    />
                  </div>
                  <div class="form-group">
                    <div class="custom-control custom-checkbox">
                      <input
                        type="checkbox"
                        class="custom-control-input"
                        id="customControlAutosizing"
                      />
                    </div>
                  </div>
                  <button
                    type="submit"
                    class="btn btn-success btn-block"
                    value="Submit"
                  >
                    REGISTER
                  </button>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- End Register -->
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      company: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      errors: null,
    };
  },
  methods: {
    submit: function() {
      var params = {
        company: this.company,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
      };
      axios
        .post("/api/users", params)
        .then((response) => {
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
