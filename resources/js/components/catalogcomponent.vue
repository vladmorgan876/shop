<template>
    <div class="fon">
    <div  class="productsINcatalog">
        <div class="products" v-for="product in products">
            <div class="card-header">
                <div class="card-text" style="color: white">{{ product.category }}</div>
            </div>
            <div class="card text-center" style="width: 18rem;">
                <img v-bind:src="'/storage/'+product.image">
                <div class="card-body ">
                    <h4 class="card-text">{{ product.name }}</h4>
                    <div class="card-text">{{ product.price }}</div>
                    <button v-on:click="addTOcart(product)" class="btn btn-outline-secondary">в корзину</button>
                </div>
            </div>
        </div>

    </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name: "catalogcomponent",

    data() {
        return {
            products: [],

        }
    },
    mounted() {
        this.getproduct();
    },
    methods: {
        getproduct: function () {
            axios.get('/api/product').then((resp) => {
                this.products = resp.data;
                // console.log(this.products)
            })
        },
        addTOcart: function (product) {
            this.$store.dispatch('TOCART', product);
        },
    }
}
</script>

<style scoped>
.fon{
    background-image: url("/storage/newimage/fon2.jpg");
    background-size: 100%;
    margin-top: 3em;
}
.productsINcatalog {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    margin-left: -3em;

}
.products {
    width: 17.4em;
    height: 28em;
    margin-top: 3em;
    margin-left: 3em;
    box-shadow: 1em 1em 2em grey;
    border: 3px solid white;
    border-radius: 0.5em;
    overflow: hidden;
}

img {
    width: 18em;
    height: 18em;
}
h4 {
    color: fuchsia;
    text-align: center;
    font-family: "Noto Sans";
}
.card-text{
    font-family: "Noto Sans";
}
.image{
    margin-right: 2em;
}
.card-body{
    margin-top: -1em;
}
</style>
