<template>
    <div class="products-list">
        <div 
            class="product"
            v-for="product in store.products"
            :key="product.id"
            @click="goToProductPage(product.id)"
        >
                <div class="pla">
                    <img :src="product.thumbnail" alt="">
                </div>
                
                <div class="lap">
                    <h2>{{ product.brand }}</h2>
                    <p>{{ product.description }}</p>
                    <p>Cena: {{ product.price}},00zł</p>
                </div>
            
            
        </div>
    </div>
</template>


<script>
import { defineComponent } from 'vue';

export default defineComponent( {
    name:'CatalogView'
})
</script>

<script setup>
import { onMounted,computed} from 'vue';
import { productsStore } from '@/stores/products';
import { useRouter } from 'vue-router';


const store = productsStore()
const router = useRouter()

const goToProductPage = (id) => {
    router.push({name: 'ProductView', params:{ id } })
}



onMounted( () => {
    store.fetchProductsFromDB()
})
</script>


<style scoped>
.products-list{
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
}
.product{
    flex-basis: 30%;
    margin: 20px 0px 20px 10px;
    padding: 16px;
    box-shadow: 0px 0px 14px 1px #e6e6e6;
    cursor: pointer;
    height: 400px;
    text-align: center;
    border-radius: 50px;
    
    transition: 0.5s;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    
}
.pla{
    height: 60%;
    width: 100%;
  
}
.pla img{
    height: 100%;
    width: 80%;
}
.lap{
    width: 100%;
    height: 40%;
    
}
.product:hover{
    scale: 0.98;
    box-shadow: 0px 0px 10px 1px #141010;;
}
</style>