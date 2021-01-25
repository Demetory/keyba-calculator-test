<template>
<div class="container">
    <div v-for="(field, index) in inputs" :key="index" :class="get_column(field)" ref="comp">
        <component
                :is="field.type"
                :value="formData[field.name]"
                :default="get_default(field)"
                :minvalue="field.minvalue"
                :maxvalue="field.maxvalue"
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

export default {
    name : 'form_params',
    components : { input_select, input_text },
    props : {
        inputs : {
            type: [Array, Object],
            required: true,
            default: null
        },
        value : {
            type: Object,
            required: true,
            default: null
        }
    },
    data() {
        return {
            formData: this.value || {}
        }
    },
    methods : {
        get_column(field){
            if (field.type && field.type === 'input_text'){ return 'form__col ' }
            else { return 'form__row ' }
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
        },
        updateForm(fieldName, value) {
            this.$set(this.formData, fieldName, value);
            this.$emit('input', this.formData);

            let price = 0

            if (fieldName == 'param_width' || fieldName == 'param_height'){
                price = value.unitprice * this.formData[fieldName].value
            }
            else {
                if (value.unitprice){ price = value.unitprice }
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
    },
    updated(){
        if (this.formData.param_profil.unitprice){
            this.$refs.comp[3].style.display = 'flex';
        }
        else {
            this.$refs.comp[3].style.display = 'none';
        }
    }
}
</script>

<style scoped>
.container { display: flex; flex-direction: row; flex-wrap: wrap; max-width: 225px; }

.form__row { margin-bottom: 20px; display: flex; width: 100%; }
.form__col { margin: 0 8px; flex-direction: column; flex: 1 1 auto; margin-bottom: 20px; }
.form__col:nth-child(1) { margin-left: 0; }
.form__col:nth-child(2) { margin-right: 0; }

.hidden { display: none; }
</style>