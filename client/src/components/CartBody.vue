<template>
  <div class="cart-body" v-if="products">
    <div class="product" v-for="product in  products" :key="product.id">
        <img class="ui image fluid" :src="API_URL + product.image.url" :alt="product.title" />
            {{products.image}}
    <div class="info">
        <p>{{product.title}}</p>
        <div class="price">
            <p>{{product.price}}€</p>
            <div class="quantity">
                <button class="ui button primary" size="large" @click="increaseProductCart(product.id)">+</button>
                <p>{{product.quantity}}</p>
                <button class="ui button primary" size="large" @click="decreaseProductCart(product.id)">-</button>
            </div>
        </div>
    </div>
    </div>
  </div>
</template>

<script>
import { API_URL } from "../utils/constants";
import { addProductCartApi, deleteProductCartApi } from "../api/card";
export default {
    name: 'CartBody',
    props:{
        products:{
            type: Array
        },
        reloadCartFn:{
            type: Function
        }
    },
    setup(props){
        const increaseProductCart = (id) =>{
            addProductCartApi(id);
            props.reloadCartFn();
        }

        const decreaseProductCart = (id) =>{
            deleteProductCartApi(id);
            props.reloadCartFn();
        }


        return{
            API_URL,
            increaseProductCart,
            decreaseProductCart
        }
    }

}
</script>

<style lang="scss" scoped>

.cart-body{
    padding: 20px 10px;
    overflow-y: scroll;
    height: calc(100vh - 10px - 90px);
    &::-webkit-scrollbar{
        display: none;
    }

.product{
    display: flex;
    .ui.image.fluid{
        width: 100px !important;
       
    }
    .info{
        display: flex;
        flex-direction: column;
        justify-content: center;
        width: 100%;
    }
    .price{
        display: flex;
        justify-content: space-between;
        p{
            margin: 0;
        }
    }
    .quantity{
        display: flex;
        align-items: center;
        p{
            margin: 0 10px;
        }
        button{
            padding: 4px 10px;
        }
    }
    }
}
</style>