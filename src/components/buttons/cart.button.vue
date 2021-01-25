<template>
    <button class="btn-cart" @click="add_to_cart()">{{ label }}</button>
</template>

<script>
export default {
    name : 'cart_button',
    props: {
        label: {
            type: String,
            required: true,
            default: null
        },
        cart: {
            type: Object,
            required: true,
            default: null
        }
    },
    methods: {
        add_to_cart(){
            console.log('Added to cart: ' + this.cart);
        }
    }
}
</script>

<style scoped>
.btn-cart { padding: 15px 0; display: flex; width: 100%; border: solid 1px #fe5c26; background-color: transparent; color: #fe5c26; font-weight: 700; text-transform: uppercase; font-size: 15px; justify-content: center; font-family: 'Roboto', sans-serif; cursor: pointer; transition: background-color .5s, color .5s; }
.btn-cart:hover { background-color: #fe5c26; color: #fff; }
</style>