<template>
  <div class="card shadow card-product">
    <img
      :src="'/assets/images/' + product.gambar"
      class="card-img-top"
      alt="aaa"
      style="height: 180px; object-fit: cover"
    />
    <div class="card-body">
      <h5 class="card-title">{{ product.nama }}</h5>
      <p class="card-text">harga : Rp. {{ product.harga }}</p>
      <router-link class="btn btn-success" :to="'/Foods/' + product.id"
        ><b-icon-cart></b-icon-cart>pesan</router-link
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script>

<style>
</style>