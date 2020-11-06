<template>
  <div class="products-new">
    <form v-on:submit.prevent="productCreate()">
      <h1>Create Product</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="productTitle" />
      </div>
      <div class="form-group">
        <label>Price:</label>
        <input type="text" class="form-control" v-model="productPrice" />
      </div>
      <div class="form-group">
        <label>/Unit:</label>
        <input type="text" class="form-control" v-model="productUnit" />
      </div>
      <div class="form-group">
        <label>Negotiable?</label>
        <input
          type="checkbox"
          class="form-control"
          v-model="productPriceNegotiable"
        />
      </div>
      <div class="form-group">
        <label>Description:</label>
        <input type="text" class="form-control" v-model="productDescription" />
      </div>
      <div class="form-group">
        <label>Image</label>
        <input
          type="file"
          class="form-control"
          v-on:change="setFile($event)"
          ref="fileInput"
        />
      </div>
      <div class="form-group">
        <label for="categories">Category:</label>
        <select name="categories" id="categories" v-model="productCategoryId">
          <option value="1">Baked goods</option>
          <option value="2">Crafts and/or woodworking items</option>
          <option value="3">Eggs</option>
          <option value="4">Fresh and/or dried herbs</option>
          <option value="5">Honey</option>
          <option value="6">Maple syrup and/or maple products</option>
          <option value="7">Nuts</option>
          <option value="8">Poultry</option>
          <option value="9">Soap and/or body care products</option>
          <option value="10">Wine, beer, hard cider</option>
          <option value="11">Dry beans</option>
          <option value="12">Grains and or flour</option>
          <option value="13">Mushrooms</option>
          <option value="14">Tofu and or non-animal protein</option>
          <option value="15">Cheese and/or dairy products</option>
          <option value="16">Cut flowers</option>
          <option value="17">Fish and/or seafood</option>
          <option value="18">Fresh vegetables</option>
          <option value="19"
            >Canned or preserved fruits, vegetables, jams, jellies, preserves,
            salsas, pickles, dried fruit, etc.</option
          >
          <option value="20">Meat</option>
          <option value="21">Plants in containers</option>
          <option value="22">Prepared foods (for immediate consumption)</option>
          <option value="23">Trees, shrubs</option>
          <option value="24">Coffee and or tea</option>
          <option value="25">Fresh fruits</option>
          <option value="26">Juices and or non-alcoholic ciders</option>
          <option value="27">Pet food</option>
          <option value="28"
            >Wild harvested forest products: mushrooms, medicinal herbs, edible
            fruits and nuts, etc.</option
          >
        </select>
      </div>
      <input type="submit" class="btn btn-primary" value="create product" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      errors: null,
      productTitle: "",
      productPrice: "",
      productPriceNegotiable: null,
      productDescription: "",
      productUnit: "",
      productImageUrl: "",
      productCategoryId: "",
    };
  },
  created: function() {},
  methods: {
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.image = event.target.files[0];
      }
    },
    productCreate: function() {
      var formData = new FormData();
      formData.append("title", this.productTitle);
      formData.append("price", this.productPrice);
      formData.append("price_negotiable", this.productPriceNegotiable);
      formData.append("description", this.productDescription);
      formData.append("unit", this.productUnit);
      formData.append("category_id", this.productCategoryId);
      if (this.image) {
        formData.append("image", this.image);
      }
      axios
        .post("/api/products", formData)
        .then((response) => {
          this.$router.push(`/users/${this.$parent.getUserId()}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
