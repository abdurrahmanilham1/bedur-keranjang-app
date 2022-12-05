<template>
  <div class="pemesanan-sukses">
    <MyNavbar />
    <div class="container">
      <div class="row justify-content-center mt-5">
        <div class="col text-center">
          <img src="../assets/images/menunggu.png" width="300" />
          <h2><strong>suksess~!!</strong></h2>
          <h4>
            Pesanan Anda Segera DI Proses <br />
            Tunggu Sebentar
          </h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MyNavbar from "@/components/MyNavbar.vue";
export default {
  name: "pemesananSukses",
  components: {
    MyNavbar,
  },
};
</script>

<style>
</style>