<template>
  <div class="home">
    <MyNavbar />
    <div class="container">
      <Hero />

      <div class="row-mt-4">
        <div class="col">
          <h2>Best <strong>Food</strong></h2>
        </div>
        <div class="col">
          <router-link to="/foods" class="btn btn-success float-right"
            ><b-icon-eye></b-icon-eye>Lihat Semua></router-link
          >
        </div>
      </div>

      <div class="row mb-4">
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
import Hero from "@/components/Hero.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    MyNavbar,
    Hero,
    CardProduct,
  },

  data() {
    return {
      products: [],
    };
  },
  methods: {
    SetProduct(data) {
      this.products = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/best-products")
      .then((response) => this.SetProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
