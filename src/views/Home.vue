<template>
  <div class="home" style="min-height:100vh;">
    <svg class="wave-home" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320"><path fill="#dc143c" fill-opacity="1" d="M0,64L60,101.3C120,139,240,213,360,240C480,267,600,245,720,213.3C840,181,960,139,1080,149.3C1200,160,1320,224,1380,256L1440,288L1440,0L1380,0C1320,0,1200,0,1080,0C960,0,840,0,720,0C600,0,480,0,360,0C240,0,120,0,60,0L0,0Z"></path></svg>
    <div>
      <Navbar />
      <Hero/>
    </div>
    
      <div class="container relative best-product mt-5">
        <div class="d-flex justify-content-between" id="best-product">
          <h2>Best Product</h2>
          <router-link to="/foods" class="btn btn-danger">
            <b-icon-eye></b-icon-eye>
            All Foods 
          </router-link>
        </div>
        <div class="row">
          <div class="col-md-4" v-for="product in products" :key="product.id" data-aos="zoom-in">
            <Card :product="product"/>
          </div>
        </div>
      </div>

      <Appstore/>


  </div>
</template>

<script>


// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import Card from '@/components/Card.vue'
import Appstore from '@/components/Appstore.vue'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Navbar,
    Hero,
    Card,
    Appstore,
  },
  data(){
    return {
      products: []
    }
  },
  methods: {
    setProducts(data) {
      this.products = data;
    }
  },
  mounted(){
    axios.get('http://localhost:3000/best-products')
    .then(response => {
      // handle respon 
      this.setProducts(response.data);
    })
    .catch(error => {
      // handle error 
      console.log(error);
    })

  }
}
</script>
