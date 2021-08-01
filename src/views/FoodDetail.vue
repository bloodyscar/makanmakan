<template>
  <div class="food-detail" style="min-height:100vh;">
    <Navbar />
    <div class="container">
      <div class="row mt-5">
        <div class="col-md-6">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <a class="text-muted" href="/">Home</a>
              </li>
              <li class="breadcrumb-item">
                <a class="text-muted" href="/foods">Products</a>
              </li>
              <li class="breadcrumb-item active">
                <a class="text-muted" href="">Product Detail</a>
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <h2 class="mt-4">Detail Makanan</h2>
      <div class="row mt-3">
        <div class="col-md-6">
          <img
            class="rounded-lg"
            :src="require(`../assets/image/${product.gambar}`)"
            width="100%"
          />
        </div>
        <div class="col">
          <h3>{{ product.nama }}</h3>
          <hr />
          <p>Harga : {{ product.harga }}</p>
          <form action="">
            <div class="form-group">
              <label for="jumlah_pemesanan" class="form-label"
                >Jumlah Pesan</label
              >
              <input
                required
                type="number"
                name="jumlah"
                id="jumlah"
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
              />
            </div>
            <div class="form-group">
              <label for="keterangan" class="form-label">Keterangan</label>
              <textarea
                required
                type="text"
                name="keterangan"
                id="keterangan"
                class="form-control"
                v-model="pesan.keterangan"
              ></textarea>
            </div>
            <button type="submit" class="btn btn-danger" @click="pemesanan">
              Order Now
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Navbar from "@/components/Navbar.vue";

export default {
  name: "FoodDetail",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.product = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$toast.success("Add to Cart Success..", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((error) => {
            console.log(error.message);
          });
      } else {
        this.$toast.error("Silahkan isi jumlah pesanan", {
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
      .then((response) => {
        this.setProduct(response.data);
      })
      .catch((error) => {
        console.log(error.message);
      });
  },
};
</script>

<style>
</style>