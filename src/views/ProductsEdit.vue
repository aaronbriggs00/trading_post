<template>
  <div class="products-new">
    <form v-on:submit.prevent="productEdit()">
      <h1>Edit Product</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="product.title" />
      </div>
      <div class="form-group">
        <label>Price:</label>
        <input type="text" class="form-control" v-model="product.price" />
      </div>
      <div class="form-group">
        <label>/Unit:</label>
        <input type="text" class="form-control" v-model="product.unit" />
      </div>
      <div class="form-group">
        <label>Negotiable?</label>
        <input
          type="checkbox"
          class="form-control"
          v-model="product.price_negotiable"
        />
      </div>
      <div class="form-group">
        <label>Description:</label>
        <input type="text" class="form-control" v-model="product.description" />
      </div>
      <div class="form-group">
        <label>Image</label>
        <input type="text" class="form-control" v-model="product.image_url" />
      </div>
      <div class="form-group">
        <label for="categories">Category:</label>
        <select name="categories" id="categories" v-model="product.category_id">
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
      <input type="submit" class="btn btn-primary" value="edit product" />
      <button class="btn btn-primary" v-on:click="deleteProduct()">
        delete
      </button>
    </form>
    <h1>{{ product }}</h1>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      errors: null,
      product: {},
    };
  },
  created: function() {
    axios.get(`/api/products/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.product = response.data;
    });
  },
  methods: {
    productEdit: function() {
      var params = {
        title: this.product.title,
        price: this.product.price,
        price_negotiable: this.product.price_negotiable,
        category_id: this.product.category_id,
        description: this.product.description,
        image_url: this.product.image_url,
        unit: this.product.unit,
      };
      axios
        .patch(`/api/products/${this.product.id}`, params)
        .then((response) => {
          this.$router.push(`/users/${this.$parent.getUserId()}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    deleteProduct: function() {
      axios
        .delete(`/api/products/${this.product.id}`)
        .then((response) => {
          this.$router.push(`/users/${this.$parent.getUserId()}`);
        })
        .catch((error) => {
          this.erros = error.response.data.errors;
        });
    },
  },
};
</script>
