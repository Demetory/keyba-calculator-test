<template>
    <label class="checkbox" v-on:click="changePrice()">Добавить москитную сетку {{ price }}
        <input type="checkbox" />
        <span class="checkmark"></span>
    </label>
</template>

<script>
export default {
    name : 'Checkbox',
    props : ['price'],
    methods: {
        changePrice(){
            this.$parent.price = this.price + 5000;
            console.log(this.price);
        }
    }
}
</script>

<style scoped>
.checkbox { margin-left: 58px; padding-left: 28px; display: flex; position: relative; cursor: pointer; user-select: none; }
.checkbox input { position: absolute; opacity: 0; cursor: pointer; height: 0; width: 0; }
.checkmark { top: -2px; left: 0; height: 16px; width: 16px; position: absolute; border: solid 2px #e6e6e6; background-color: #fff; transition: background-color .5s; }
.checkbox:hover input ~ .checkmark { background-color: #f3f3f3; }
.checkbox input:checked ~ .checkmark { background-color: #fe5c26; }
.checkbox input:checked ~ .checkmark:after { display: flex; }
</style>