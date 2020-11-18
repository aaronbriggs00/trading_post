<template>
  <div class="users-edit">
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
                <router-link
                  class="text-white"
                  v-if="$parent.getUserId() == $route.params.id"
                  :to="`/users/${$route.params.id}`"
                  >View Profile</router-link
                >
                /
                <span class="text-success">Edit Profile</span>
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- End Inner Header -->
    <!-- Tabs -->
    <section class="tab-view">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <ul class="nav justify-content-center">
              <li class="nav-item">
                <a class="nav-link active text-success">Edit Profile</a>
              </li>
              <li class="nav-item">
                <router-link class="nav-link" to="/products/new"
                  >Add Product</router-link
                >
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    <!-- End Tabs -->
    <!-- Edit Profile -->
    <section class="section-padding">
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-8 mx-auto">
            <form id="edit" v-on:submit.prevent="submit()">
              <div class="card padding-card">
                <div class="card-body">
                  <div v-for="error in errors">
                    <p class="text-danger">{{ error }}</p>
                  </div>
                  <h5 class="card-title mb-4">Profile Information</h5>
                  <div class="form-group">
                    <label
                      >Company Name <span class="text-danger">*</span></label
                    >
                    <input
                      type="text"
                      class="form-control"
                      v-model="user.company"
                    />
                  </div>
                  <div class="form-group">
                    <label
                      >Company Description
                      <span class="text-danger">*</span></label
                    >
                    <textarea
                      v-model="user.bio"
                      class="form-control"
                      rows="4"
                    ></textarea>
                  </div>
                  <div class="row">
                    <div class="form-group col-md-4">
                      <label>Email <span class="text-danger">*</span></label>
                      <input
                        type="text"
                        class="form-control"
                        v-model="user.email"
                      />
                    </div>
                    <div class="form-group col-md-4">
                      <label>Website <span class="text-danger">*</span></label>
                      <input
                        type="text"
                        class="form-control"
                        v-model="user.website"
                      />
                    </div>
                    <div class="form-group col-md-4">
                      <label>Phone <span class="text-danger">*</span></label>
                      <input
                        type="text"
                        class="form-control"
                        v-model="user.phone_number"
                      />
                    </div>
                  </div>
                  <div class="row">
                    <div class="form-group col-md-8">
                      <label>address <span class="text-danger">*</span></label>
                      <input
                        type="text"
                        class="form-control"
                        v-model="user.address"
                      />
                    </div>
                  </div>
                  <div class="row">
                    <div class="col-md-6">
                      <label
                        >Profile Image <span class="text-danger"></span></label
                      ><br />
                      <span v-if="image" class="text-success"
                        >file successfully uploaded!</span
                      >
                      <div class="fuzone">
                        <div class="fu-text">
                          <span
                            ><i class="mdi mdi-image-area"></i> Click here or
                            drop files to upload</span
                          >
                        </div>
                        <input
                          v-on:change="setFile($event)"
                          class="upload"
                          type="file"
                        />
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <button type="submit" class="btn btn-success">
                Save Profile
              </button>
            </form>
            <form id="edit" v-on:submit.prevent="submitPassword()">
              <div class="card padding-card">
                <div class="card-body">
                  <h5 class="card-title mb-4">Change Password</h5>
                  <div class="row">
                    <div class="form-group col-md-4">
                      <label>Password <span class="text-danger">*</span></label>
                      <input
                        type="password"
                        class="form-control"
                        v-model="password1"
                      />
                      <br />
                      <p v-if="password1 != '' && password1.length < 6">
                        password must exceed 6 characters
                      </p>
                    </div>

                    <div class="form-group col-md-4">
                      <label
                        >Password Confirmation
                        <span class="text-danger">*</span></label
                      >
                      <input
                        type="password"
                        class="form-control"
                        v-model="password2"
                      />
                      <br />
                      <p v-if="password1 != password2">passwords must match!</p>
                    </div>
                  </div>
                </div>
              </div>
              <button type="submit" class="btn btn-success">
                Change Password
              </button>
            </form>
            <form id="edit" v-on:submit.prevent="deleteUser()">
              <button type="submit" class="btn btn-success">
                Delete Account
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>
    <!-- End Edit Profile -->
  </div>
</template>

<style>
#edit {
  padding-bottom: 14px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      user: {},
      errors: null,
      showPasswordForm: false,
      password1: "",
      password2: "",
      password: null,
      passwordFormMessage: null,
      dontReturnToShow: false,
      image: null,
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
    });
  },
  methods: {
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.image = event.target.files[0];
      }
    },
    submit: function() {
      var formData = new FormData();
      formData.append("first_name", this.user.first_name);
      formData.append("last_name", this.user.last_name);
      formData.append("company", this.user.company);
      formData.append("address", this.user.address);
      formData.append("bio", this.user.bio);
      formData.append("email", this.user.email);
      if (this.password) {
        formData.append("password", this.password);
      }
      formData.append("phone_number", this.user.phone_number);
      formData.append("website", this.user.website);
      if (this.image) {
        formData.append("image", this.image);
      }
      axios
        .patch(`/api/users/${this.$route.params.id}`, formData)
        .then((response) => {
          if (this.dontReturnToShow == false) {
            this.$router.push(`/users/${this.$route.params.id}`);
          }
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    submitPassword: function() {
      this.passwordCheck();
      var formData = new FormData();
      if (this.password) {
        formData.append("password", this.password);
      }
      axios
        .patch(`/api/users/${this.$route.params.id}`, formData)
        .then((response) => {
          if (this.dontReturnToShow == false) {
            this.$router.push(`/users/${this.$route.params.id}`);
          }
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    passwordCheck: function() {
      if (this.password1 === this.password2 && this.password1.length > 6) {
        this.password = this.password1;
        this.password1 = "";
        this.password2 = "";
      } else {
        this.passwordFormMessage = "please check your password inputs";
      }
    },
    deleteUser: function() {
      if (
        confirm(
          "This will delete your account and any information will not be saved. Are you sure?"
        )
      ) {
        axios
          .delete(`/api/users/${this.user.id}`)
          .then((response) => {
            localStorage.removeItem("jwt");
            localStorage.removeItem("user_id");
            this.$router.push("/home");
          })
          .catch((error) => {
            this.erros = error.response.data.errors;
          });
      }
    },
    passwordToggle: function() {
      if (this.showPasswordForm === false) {
        this.showPasswordForm = true;
      } else {
        this.showPasswordForm = false;
      }
    },
  },
};
</script>
