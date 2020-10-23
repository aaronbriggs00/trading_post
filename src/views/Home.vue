<template>
  <div class="home">
    <h1 v-if="$parent.isLoggedIn()">{{ message }}</h1>
  </div>
</template>

<style></style>

<script>
export default {
  data: function() {
    return {
      message: "You're logged in!!!",
    };
  },
  created: function() {},
  methods: {},
};
</script>
