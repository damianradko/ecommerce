<template>
  <header>
    <div class="welcome">
      <img @click="router.push({name:'Catalog'})" src="@/img/logo.png" alt="">
    </div>
    <div class="cart-items" @click="router.push({name: 'CartView'})">
      <img src="@/img/cart.png" alt="">
      <p> Koszyk: {{ store.cart.length }}</p>
    </div>
  </header>
  <main>
      <RouterView />
  </main>
</template>

<script setup>
import {RouterView, useRouter } from 'vue-router';
import { productsStore } from '@/stores/products';

const router = useRouter()
const store = productsStore()

</script>



<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
*{
  font-family: 'Roboto', sans-serif;
}
.welcome{
  width: 80%;
 
}
.welcome img{
  height: 100px;
  cursor: pointer;
}
.cart-items{
  justify-content: end;
  align-items: center;
  padding: 16px;
  font-weight: bold;
  font-size: 24px;
  cursor: pointer;
  width: 20%;
  display: flex;
}
.cart-items img{
  width: 40px;
  height: 40px;
}
header{
  display: flex;
}

</style>
