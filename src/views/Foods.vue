<template>
  <div>
    <MyNavbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h2>Daftar <strong>Makanan</strong></h2>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon1"
              ><b-icon-search></b-icon-search
            ></span>
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="search your favorite food"
              aria-label="search your favorite food"
              aria-describedby="basic-addon1"
              @keyup="searchFood"
            />
          </div>
        </div>
      </div>

      <div class="row mb-3">
        <div
          class="col-md-4 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import MyNavbar from "@/components/MyNavbar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "MyFoods",
  components: {
    MyNavbar,
    CardProduct,
  },
  data() {
    return {
      products: [],
      search: "",
    };
  },
  methods: {
    SetProduct(data) {
      this.products = data;
    },
    searchFood() {
      axios
        .get("http://localhost:3000/products?q=" + this.search)
        .then((response) => this.SetProduct(response.data))
        .catch((error) => console.log(error));
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products")
      .then((response) => this.SetProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>