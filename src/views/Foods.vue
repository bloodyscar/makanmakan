<template>
  <div class="foods">
    <Navbar/>
    <div class="container" style="margin-top: 100px;">
      <h2>Daftar Makanan</h2>
      <div class="input-group mb-3 mt-3">
        <input v-model="search" type="text" class="form-control" placeholder="Cari makanan" aria-label="Cari makanan" aria-describedby="basic-addon1" @keyup="searchFood">
        <div class="input-group-prepend">
          <span class="input-group-text" id="basic-addon1"><b-icon-search></b-icon-search></span>
        </div>
      </div>
      
      <div class="row">
        <div class="col-md-4" v-for="product in products" :key="product.id">
          <Card :product="product"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import Card from '@/components/Card.vue'

import axios from 'axios'


export default {
  name: 'Foods',
  components:{
    Navbar,
    Card
  },
  data(){
    return{
      products: [],
      search: '',
    }
  },
  methods:{
    setProducts(data){
      this.products = data;
    },
    searchFood(){
    axios.get('http://localhost:3000/products?q=' + this.search)
    .then(response => {
      this.setProducts(response.data);
    })
    .catch(error => {
      console.log(error.message);
    });
    }
  },
  mounted(){
    axios.get('http://localhost:3000/products')
    .then(response => {
      this.setProducts(response.data);
    })
    .catch(error => {
      console.log(error.message);
    });
  }
}
</script>

<style>

</style>