<template>
  <div class="products-new">
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
                  :to="`/users/${product.user_id}`"
                  >View Profile</router-link
                >
                /
                <router-link
                  class="text-white"
                  :to="`/users/${product.user_id}/edit`"
                  >Edit Profile</router-link
                >
                /
                <span class="text-success">Edit Product</span>
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
                <a class="nav-link active text-success">Edit Product</a>
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
    <!-- Edit Product -->
    <section class="section-padding">
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-8 mx-auto">
            <form id="edit" v-on:submit.prevent="productEdit()">
              <div class="card padding-card">
                <div class="card-body">
                  <h5 class="card-title mb-4">Profile Information</h5>
                  <div class="form-group">
                    <label
                      >Product Name <span class="text-danger">*</span></label
                    >
                    <input
                      type="text"
                      class="form-control"
                      v-model="product.title"
                    />
                  </div>
                  <div class="form-group">
                    <label
                      >Product Description
                      <span class="text-danger">*</span></label
                    >
                    <textarea
                      class="form-control"
                      rows="4"
                      v-model="product.description"
                    ></textarea>
                  </div>
                  <div class="row">
                    <div class="form-group col-md-4">
                      <label>Price <span class="text-danger">*</span></label>
                      <input
                        v-model="product.price"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    /
                    <div class="form-group col-md-4">
                      <label
                        >Unit Pricing<span class="text-danger"></span
                      ></label>
                      <select
                        v-model="product.unit"
                        class="form-control custom-select"
                      >
                        <option>Select unit</option>
                        <option value="lbs">lbs</option>
                        <option value="oz">oz</option>
                        <option value="gallon">gallon</option>
                        <option value="liter">liter</option>
                      </select>
                    </div>
                    <div id="checkbox" class="form-group col-md-3">
                      <div class="custom-control custom-checkbox">
                        <input
                          type="checkbox"
                          class="custom-control-input"
                          id="osahan-checkbox"
                          v-model="product.price_negotiable"
                        />
                        <label
                          class="custom-control-label"
                          for="osahan-checkbox"
                          >Price Negotiable</label
                        >
                      </div>
                    </div>
                  </div>
                  <div class="row">
                    <div class="form-group col-md-4">
                      <label>Category<span class="text-danger">*</span></label>
                      <select
                        v-model="product.category.id"
                        class="form-control custom-select"
                      >
                        <option value="1">Baked goods</option>
                        <option value="2"
                          >Crafts and/or woodworking items</option
                        >
                        <option value="3">Eggs</option>
                        <option value="4">Fresh and/or dried herbs</option>
                        <option value="5">Honey</option>
                        <option value="6"
                          >Maple syrup and/or maple products</option
                        >
                        <option value="7">Nuts</option>
                        <option value="8">Poultry</option>
                        <option value="9"
                          >Soap and/or body care products</option
                        >
                        <option value="10">Wine, beer, hard cider</option>
                        <option value="11">Dry beans</option>
                        <option value="12">Grains and or flour</option>
                        <option value="13">Mushrooms</option>
                        <option value="14"
                          >Tofu and or non-animal protein</option
                        >
                        <option value="15">Cheese and/or dairy products</option>
                        <option value="16">Cut flowers</option>
                        <option value="17">Fish and/or seafood</option>
                        <option value="18">Fresh vegetables</option>
                        <option value="19"
                          >Canned or preserved fruits, vegetables, jams,
                          jellies, preserves, salsas, pickles, dried fruit,
                          etc.</option
                        >
                        <option value="20">Meat</option>
                        <option value="21">Plants in containers</option>
                        <option value="22"
                          >Prepared foods (for immediate consumption)</option
                        >
                        <option value="23">Trees, shrubs</option>
                        <option value="24">Coffee and or tea</option>
                        <option value="25">Fresh fruits</option>
                        <option value="26"
                          >Juices and or non-alcoholic ciders</option
                        >
                        <option value="27">Pet food</option>
                        <option value="28"
                          >Wild harvested forest products: mushrooms, medicinal
                          herbs, edible fruits and nuts, etc.</option
                        >
                      </select>
                    </div>
                  </div>
                  <div class="row">
                    <div class="col-md-6">
                      <label
                        >Product Image <span class="text-danger"></span
                      ></label>
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
                Edit Product
              </button>
            </form>
            <form id="edit" v-on:submit.prevent="deleteProduct()">
              <button type="submit" class="btn btn-success">
                Delete Product
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>
    <!-- End Edit Product -->
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
        <input
          type="file"
          class="form-control"
          v-on:change="setFile($event)"
          ref="fileInput"
        />
      </div>
      <div class="form-group">
        <label for="categories">Category:</label>
        <select name="categories" id="categories" v-model="product.category.id">
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
  </div>
</template>

<style>
#checkbox {
  padding-top: 32px;
}
</style>

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
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.image = event.target.files[0];
      }
    },
    productEdit: function() {
      var formData = new FormData();
      formData.append("title", this.product.title);
      formData.append("price", this.product.price);
      formData.append("price_negotiable", this.product.price_negotiable);
      formData.append("description", this.product.description);
      if (this.product.unit) {
        formData.append("unit", this.product.unit);
      }
      formData.append("category_id", this.product.category.id);
      if (this.image) {
        formData.append("image", this.image);
      }
      axios
        .patch(`/api/products/${this.product.id}`, formData)
        .then((response) => {
          this.$router.push(`/users/${this.$parent.getUserId()}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    deleteProduct: function() {
      if (confirm("This will delete your product forever. Are you sure?")) {
        axios
          .delete(`/api/products/${this.product.id}`)
          .then((response) => {
            this.$router.push(`/users/${this.$parent.getUserId()}`);
          })
          .catch((error) => {
            this.erros = error.response.data.errors;
          });
      }
    },
  },
};
</script>
