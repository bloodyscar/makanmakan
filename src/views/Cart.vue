<template>
  <div class="food-detail">
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
                <a class="text-muted" href="#">Cart</a>
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <h2 class="mt-4">Keranjang Makanan</h2>
    <div class="row">
        <div class="col">
            <table class="table">
                <thead>
                    <tr>
                    <th scope="col">No</th>
                    <th scope="col">Foto</th>
                    <th scope="col">Makanan</th>
                    <th scope="col">Keterangan</th>
                    <th scope="col">Jumlah</th>
                    <th scope="col">Harga</th>
                    <th scope="col">Total Harga</th>
                    <th scope="col">Hapus</th>

                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(keranjang, index) in keranjang" :key="keranjang.id">
                    <th scope="row">{{index+1}}</th>
                    <td>
                        <img :src="require(`../assets/image/${keranjang.product.gambar}`)" width="250"/>
                    </td>
                    <td>{{ keranjang.product.nama }}</td>
                    <td>{{ !keranjang.keterangan ? '-' : keranjang.keterangan}}</td>
                    <td>{{ keranjang.jumlah_pemesanan }}</td>
                    <td>{{ keranjang.product.harga }}</td>
                    <td>{{ keranjang.product.harga * keranjang.jumlah_pemesanan }}</td>
                    <td @click="hapusKeranjang(keranjang.id)"><a href=""><b-icon-trash class="text-danger"></b-icon-trash></a></td>
                    </tr>
                    <tr>
                        <td colspan="7" align="right">Total Harga :</td>
                        <td>{{ totalHarga }}</td>
                    </tr>
                </tbody>
            </table>
            <div class="row justify-content-end">
              <div class="col-md-4">
                <form>
                  <div class="form-group">
                    <label for="nama">Nama</label>
                    <input type="text" name="nama" id="nama" class="form-control" v-model="pesan.nama">
                  </div>
                  <div class="form-group">
                    <label for="noMeja">No. Meja</label>
                    <input type="text" name="noMeja" id="noMeja" class="form-control" v-model="pesan.noMeja">
                  </div>
                  <rot type="submit" class="btn btn-danger" @click="checkout">Order</rot>
              </form>
              </div>
            </div>
            
        </div>
    </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from 'axios';

export default {
    name: 'Cart',
    components: {
        Navbar
    },
    data(){
        return {
            keranjang: [],
            pesan: {},
        }
    },
    methods:{
        setKeranjang(data){
            this.keranjang = data;
            console.log(this.keranjang);
        },
        hapusKeranjang(id){
          axios.delete('http://localhost:3000/keranjangs/'+id)
          .then(() => {
            this.$toast.error("Berhasil hapus pesanan..", {
              type: "error",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
            axios.get('http://localhost:3000/keranjangs')
            .then(response => {
                this.setKeranjang(response.data)
            })
            .catch(error => {
                console.log(error.message);
            })
          })
        },
        checkout() {
      if (this.pesan.nama && this.pesan.noMeja) {
        this.pesan.keranjang = this.keranjang;
        axios
          .post("http://localhost:3000/pesanans", this.pesan)
          .then(() => {
            // Hapus Semua Keranjang 
            this.keranjang.map(function (item) {
              return axios
                .delete("http://localhost:3000/keranjangs/" + item.id)
                .catch((error) => console.log(error));
            });
            this.$router.push({ path: "/checkout-success" });
            this.$toast.success("Sukses Dipesan", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Nama dan Nomor Meja Harus diisi", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
    },
    mounted(){
        axios.get('http://localhost:3000/keranjangs')
        .then(response => {
            this.setKeranjang(response.data)
        })
        .catch(error => {
            console.log(error.message);
        })
    },
    computed : {
      totalHarga(){
        return this.keranjang.reduce((a, b) => {
          return a+(b.product.harga * b.jumlah_pemesanan)
        }, 0)
      }
      
    }
  }
</script>

<style>

</style>