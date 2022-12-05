<template>
  <div class="food-detail">
    <MyNavbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/Foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col-md-6">
          <img
            :src="'../assets/images/' + product.gambar"
            class="img-fluid shadow"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Harga: <strong>Rp.{{ product.harga }}</strong>
          </h4>
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="Jumlah Pemesanan"> Jumlah Pesan </label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
              />
            </div>
            <div class="form-group">
              <label for="Keterangan">Keterangan</label>
              <textarea
                v-model="pesan.keterangan"
                class="form-control"
                placeholder="keterangan spt : pedes , nasi setengah .."
              ></textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart>pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MyNavbar from "@/components/MyNavbar.vue";
import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    MyNavbar,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },
  methods: {
    SetProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({ path: "/keranjang" });
            this.$toast.success("sukses masuk keranjang cuy", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("jumlah pesanan harus diisi woii", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.SetProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>