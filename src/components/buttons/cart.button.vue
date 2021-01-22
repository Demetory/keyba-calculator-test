<template>
    <button class="calc__button">{{ label }}</button>
</template>

<script>
export default {
    name : 'Button_Cart',
    props: ['label']
}
</script>

<style scoped>
.calc__button { padding: 15px 0; display: flex; flex: 1; border: solid 1px #fe5c26; background-color: transparent; color: #fe5c26; font-weight: 700; text-transform: uppercase; font-size: 15px; justify-content: center; font-family: 'Roboto', sans-serif; cursor: pointer; transition: background-color .5s, color .5s; }
.calc__button:hover { background-color: #fe5c26; color: #fff; }
</style>