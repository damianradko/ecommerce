<template>
    <button @click="router.push({name: 'Catalog'})"> ⇦ Wróć</button>
   <div class="product">
        <div class="product-image">
            <img :src="selectedProduct.thumbnail" alt="">
        </div>

        <div class="details">
            <p>Marka: {{ selectedProduct.brand }}</p>
            <p>Opis: {{ selectedProduct.description }}</p>
            <h2>Cena {{ selectedProduct.price }},00zł</h2>
            <button class="ll" @click="addToCart">Dodaj Do Koszyka</button>
        </div>
   </div>
</template>

<script>
import { defineComponent, } from 'vue';

export default defineComponent({
    name:'ProductDetails'
})
</script>

<script setup>
import {computed} from 'vue';
import {productsStore} from '@/stores/products'
import { useRoute,useRouter} from 'vue-router';

const store = productsStore()
const route = useRoute()
const router = useRouter()

const selectedProduct = computed( () => {
    return store.products.find((item) => item.id === Number(route.params.id))
})

const addToCart = () => {
    store.addToCart(selectedProduct.value)
    router.push({name: 'CartView'})
}
</script>

<style scoped>
.product{
    display: flex;
    margin-top: 50px;
}
.product-image{
    margin-right: 24px;
   
}
.product-image img{
    max-height: 300px;
    min-width: 500px;
}
button{
    width: 100px;
    height: 30px;
    border-radius: 5px;
    outline: 2px solid orange;
    border:none;
    background-color: rgb(25, 170, 25);
    font-size:15px;
    cursor: pointer;
    transition: 0.5s;
    font-weight: bold;
}
button:hover{
 outline: 10px solid white;
 border: 1px solid white;
}
.ll{
    width: 150px;
}
@media(max-width:800px) {
    .product{
        width: 100%;
        height: 500px;
        
        flex-direction: column;
        text-align: center;
    }
    .product-image{
        width: 100%;
        margin: 0px;
    }
    .product-image img{
        width: 100%;
    }
}
</style>