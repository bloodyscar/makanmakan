<template>
    <nav class="navbar navbar-expand-lg navbar-light">
        <div class="container">
            <a class="navbar-brand font-weight-bold logo" href="#">FreshEat!</a>
            <button
            class="navbar-toggler"
            type="button"
            data-toggle="collapse"
            data-target="#navbarNav"
            aria-controls="navbarNav"
            aria-expanded="false"
            aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item">
                        <router-link class="nav-link" to="/">Home</router-link>
                    </li>
                    <li class="nav-item">
                        <router-link class="nav-link" to="/foods">Foods</router-link>
                    </li>
                </ul>
                <ul class="navbar-nav ml-auto">
                    <li class="nav-item">
                        <router-link class="nav-link" to="/cart">Cart
                            <b-icon-cart></b-icon-cart>
                            <span class="badge badge-primary ml-1">{{ jumlah_pesanan.length}}</span>
                        </router-link>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>

<script>
import axios from 'axios';
export default {
    name: "Navbar",
    data(){
        return{
            jumlah_pesanan:[],
        }
    },
    methods:{
        setJumlah(data){
            this.jumlah_pesanan = data;
        }
    },
    mounted(){
        axios.get('http://localhost:3000/keranjangs')
        .then((response) => {
            this.setJumlah(response.data);
        })
        .catch((error) => {
            console.log(error.message);
        })
    }
};
</script>

<style>
</style>