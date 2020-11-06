<template>
  <div class="users-edit">
    <form v-on:submit.prevent="submit()">
      <h1>Edit</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>First name:</label>
        <input type="text" class="form-control" v-model="user.first_name" />
      </div>
      <div class="form-group">
        <label>Last name:</label>
        <input type="text" class="form-control" v-model="user.last_name" />
      </div>
      <div class="form-group">
        <label>Email:</label>
        <input type="email" class="form-control" v-model="user.email" />
      </div>
      <div class="form-group">
        <label>Company:</label>
        <input type="text" class="form-control" v-model="user.company" />
      </div>
      <div class="form-group">
        <label>Address:</label>
        <input type="text" class="form-control" v-model="user.address" />
      </div>
      <div class="form-group">
        <label>Bio:</label>
        <input type="text" class="form-control" v-model="user.bio" />
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="user.image_url" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
    <button v-on:click="passwordToggle()">change password</button>
    <button class="btn btn-primary" v-on:click="deleteUser()">
      Delete Account</button
    ><br />
    <div v-if="showPasswordForm">
      <p v-if="passwordFormMessage">{{ passwordFormMessage }}</p>
      <p>enter your new password:</p>
      <input v-model="password1" type="password" /><br />
      <p v-if="password1 != '' && password1.length < 6">
        password must exceed 6 characters
      </p>
      <p>enter your password again:</p>
      <input v-model="password2" type="password" /><br />
      <p v-if="password1 != password2">passwords must match!</p>
      <button v-on:click="passwordCheck()">confirm</button>
    </div>
  </div>
</template>

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
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
    });
  },
  methods: {
    submit: function() {
      var params = {
        first_name: this.user.first_name,
        last_name: this.user.last_name,
        company: this.user.company,
        address: this.user.address,
        bio: this.user.bio,
        image_url: this.user.image_url,
        email: this.user.email,
        password: this.password,
      };
      axios
        .patch(`/api/users/${this.$route.params.id}`, params)
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
        this.dontReturnToShow = true;
        this.submit();
        this.password1 = "";
        this.password2 = "";
        this.passwordToggle();
      } else {
        this.passwordFormMessage = "please check your password inputs";
      }
    },
    deleteUser: function() {
      confirm(
        "This will delete your account and any information will not be saved. Are you sure?"
      );
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
