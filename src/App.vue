<template>
    <Calculator />
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
    name: 'App',
    components: { Calculator }
}
</script>

<style>
#calculator { margin: 0 auto; padding: 0 0 40px 0; max-width: 794px; display: flex; flex-direction: column; background-color: #f3f3f3; text-align: left; }
</style>
