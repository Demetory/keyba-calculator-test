<template>
<div>
    <p v-if="label" class="input__label">{{ label }}</p>
    <input type="text" class="input__text" :class="{ 'input__text-error' : isError }"
        :id="name"
        :name="name"
        :value="selected.value"
        :placeholder="placeholder"
        @input = "change(name, $event.target.value)"
    >
</div>
</template>

<script>
export default {
    name: 'input_text',
    props: {
        name: {
            type: String,
            required: true,
            default: null
        },
        label: {
            type: String,
            required: false,
            default: null
        },
        placeholder: {
            type: String,
            required: false,
            default: null
        },
        default: {
            type: Number,
            required: false,
            default: null
        },
        minvalue: {
            type: Number,
            required: true,
            default: 0
        },
        maxvalue: {
            type: Number,
            required: true,
            default: 0
        },
        unitprice: {
            type: Number,
            required: true,
            default: 0
        }
    },
    data(){
        return {
            selected : { 
                'value' : this.default
                    ? this.default
                    : null,
                'unitprice' : this.unitprice
            },
            isError : false
        }
    },
    methods: {
        change(field, value){
            value = Number.parseInt(value, 10);

            if (isNaN(parseFloat(value)) == true || !value || value < this.minvalue || value > this.maxvalue){ this.isError = true; value = 0; }
            else { this.isError = false; }
            
            this.selected.value = value 
            this.$emit("input", { 'value' : value, 'unitprice' : this.unitprice });
        }
    },
    mounted(){
        this.$emit("input", this.selected);
    }
}
</script>

<style scoped>
.input__label { display: block; width: 100%; padding-bottom: 10px; color: #19191a; font-size: 14px; }

.input__text { padding: 10px 20px; display: flex; width: 60px; color: #000; font-size: 14px; background-color: #fff; border: solid 2px transparent; transition: all .5s; }
.input__text:focus { border: solid 2px #fe5c26; }
.input__text-error { background-color: #ffbfbf; border: solid 2px transparent; }
</style>