<template>
    <button @click="router.push({name:'Catalog'})">⇦ Wróć</button>
    <div
    v-if="!store.cart.length"
    style="text-align: center;"
    >
        <h1>Koszyk jest pusty...</h1>
    </div>

    <div
    class="cart-items"
    v-else=""
    >
        <div 
        class="cart-item"
        v-for="item in store.cart"
        @key="item.id"
        >
            <div class="item-details">
                <img :src="item.thumbnail" alt="">
                <span>Marka {{ item.brand  }}</span>
                <span>Kategoria {{ item.category  }}</span>
                <span>Cena {{ item.price  }},00zł</span>
                <button @click="removeFromCart(item.id)">Usuń</button>
            </div>
        </div>
    </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
    name:'CartView'
})
</script>

<script setup>
import { productsStore } from '../stores/products';
import { useRouter } from 'vue-router';

const router = useRouter()

const store = productsStore()

const removeFromCart = (id) => {
    store.removeFromCart(id)
}

</script>

<style>
.item-details{
    display:flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 32px;
    box-shadow: 0 0 17px 6px #e7e7e7;
    border-radius: 8px;
    padding: 16px;
    max-height: 300px;
}
.item-details img{
    width: 20%;
    max-height: 300px; 
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
    margin-bottom: 10px;
}
button:hover{
 outline: 10px solid white;
 border: 1px solid white;
}
@media(max-width:800px){
    .item-details{
        font-size: 15px;
    }
}
</style>