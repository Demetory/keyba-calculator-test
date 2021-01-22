<template>
    <span class="calc__window-button">{{ label }}</span>
</template>

<script>
export default {
    name : 'Button_Window',
    props: ['label']
}
</script>

<style scoped>
.calc__window-button { border-radius: 50%; width: 44px; height: 44px; display: flex; align-items: center; justify-content: center; cursor: pointer; background-color: #e6e6e6; font-size: 30px; font-weight: 700; color: #fff; z-index: 10; }
</style>