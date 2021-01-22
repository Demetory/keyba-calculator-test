<template>
    <label class="calc__input-label" :for="data[0]">{{ data[1] }}, мм</label>
    <input type="text" class="calc__input" :id="data[0]" :name="data[0]" value="1300" />
</template>

<script>
export default {
    name : 'Text',
    props : ['data']
}
</script>

<style scoped>
.calc__input-label { display: block; width: 100%; padding-bottom: 10px; color: #19191a; font-size: 14px; }
.calc__input { padding: 10px 20px; display: flex; width: 50px; color: #000; font-size: 14px; background-color: #fff; border: solid 2px transparent; }
.calc__input:focus { border: solid 2px #fe5c26; }
</style>