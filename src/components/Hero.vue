<template>
    <div class="hero">

    <!-- desktop  -->
    <div class="container mt-5 d-none d-md-block" data-aos="zoom-in-up">
        <div class="row align-items-center">
            <div class="col-md-6">
                <div style="font-size:2.5vw;">
                    <strong >What are you waiting?</strong> <br />
                    Get in your App
                </div>
                <p class="text-muted" style="font-size:1vw;">Choose your favourite foods and just waiting</p>
                <div>
                <a href="#best-product" class="btn btn-primary btn-lg">Check Now</a>
                </div>
        </div>
            <div class="col-md-6">
                <img src="../assets/image/Hero.png" width="100%" class="rounded-lg" />
            </div>
        </div>
    </div>

    <!-- mobile -->
    <div class="container mt-5 d-sm-block d-md-none">
        <div class="row align-items-center">
        <div class="col-md-6">
            <img src="../assets/image/Hero.png" width="100%" />
        </div>
        <div class="col-md-6">
            <div class="h2 text-center" style="font-size:1em;">
                <strong>Tasty Foods Menu</strong> <br />
                in your App
                <div class="mt-2 text-muted text-center" style="font-size:1em;">Choose your favourite foods and just waiting</div>
            </div>
            <div class="container d-flex justify-content-center">
            <a href="#best-product" class="btn btn-primary btn-md">Check Now</a>
            </div>
        </div>
        </div>
    </div>
    

    </div>
</template>

<script>
export default {
  name: "Hero",
};
</script>

<style>
</style>