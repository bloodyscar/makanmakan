<template>
    <div>
        <div class="container mt-3">
            <div class="row">
                    <div class="card overflow-hidden">
                        <div class="overflow-hidden">
                            <router-link :to="'/foods/'+product.id"><img class="img-card" :src="require(`../assets/image/${product.gambar}`)" width="100%"></router-link>
                        </div>
                        <div class="card-body">
                            <div>
                                <p>Nama: {{product.nama}}</p>
                                <p>Harga : {{ product.harga }}</p>
                            </div>
                            <router-link :to="'/foods/'+product.id" class="btn btn-md btn-danger">
                                <b-icon-cart></b-icon-cart>
                                Order
                            </router-link>
                        </div>
                    </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['product']
}
</script>

<style>

</style>