<template>
<div class="container">
    <div v-for="(field, index) in inputs" :key="index" :class="get_column(field)">
        <component
                :is="field.type"
                :value="formData[field.name]"
                :default="get_default(field)"
                :tabindex="index"
                v-bind="field"
                @input="updateForm(field.name, $event)"
        />
    </div>
</div>
</template>

<script>
import input_select from '@/components/inputs/input_select.vue'
import input_text from '@/components/inputs/input_text.vue'
import input_checkbox from '@/components/inputs/input_checkbox.vue'

export default {
    name : 'form_window',
    components : { input_select, input_text, input_checkbox },
    props : ['inputs', 'value'],
    data() {
        return {
            formData: this.value || {}
        }
    },
    methods : {
        get_column(field){
            if (field.type && field.type === 'input_text'){ return 'form__col' }
            else { return 'form__row' }
        },
        get_default(field){
            if (field.options){
                for (let i=0; i < field.options.length; i++){
                    if (field.options[i].selected){ return field.options[i] }
                }
            }
            if (field.minvalue){
                return field.minvalue
            }
            if (field.selected){
                return field.selected
            }
        },
        updateForm(fieldName, value) {
            this.$set(this.formData, fieldName, value);
            this.$emit('input', this.formData);

            let price = 0

            if (fieldName == 'param_mosquito' && value.value === true){
                price = value.unitprice
            }
            else if (fieldName == 'param_mosquito' && value.value !== true){
                price = 0
            }
            else {
                price = value.unitprice
            }

            const param = { 'name' : fieldName, 'price' : price }
            const index = this.formData.new_price.findIndex(p => p.name === param.name)

            if (index === -1){ this.formData.new_price.push(param) } 
            else {
                this.formData.new_price[index] = param;
            }

            let  new_price = 0;
            for (let a = 0; a < this.formData.new_price.length; a++){
                new_price = new_price + this.formData.new_price[a].price
            }
            this.formData.price = new_price
        }
    }
}
</script>

<style scoped>
.container { display: flex; flex-direction: row; flex-wrap: wrap; }

.form__row { margin-bottom: 20px; display: flex; width: 100%; }
.form__col { margin: 0 8px; flex-direction: column; flex: 1 1 auto; margin-bottom: 20px; }
.form__col:nth-child(1) { margin-left: 0; }
.form__col:nth-child(2) { margin-right: 0; }
</style>