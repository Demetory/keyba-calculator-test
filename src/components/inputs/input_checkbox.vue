<template>
    <p class="form__row">
        <label class="form__checkbox">{{ label }}
            <input type="checkbox" 
                :id="name"
                :name="name"
                :checked="selected.value"
                @click = "change(name, $event.target.checked)"
            />
            <span class="form__checkmark"></span>
        </label>
    </p>
</template>

<script>
export default {
    name: 'input_checkbox',
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
        default: {
            type: Boolean,
            required: false,
            default: null
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
                    : false,
                'unitprice' : this.unitprice
            }
        }
    },
    methods : {
        change(field, value){
            this.$emit("input", { 'value' : value, 'unitprice' : this.unitprice });
        }
    },
    mounted() {
        this.$emit("input", this.selected);
    }
}
</script>

<style scoped>
.form__row { display: flex; font-size: 13px; color: #707070; align-items: center; }
.calc__params-mosquito { display: flex; font-size: 13px; color: #707070; align-items: center; }

.form__checkbox { margin-left: 58px; padding-left: 28px; display: flex; position: relative; cursor: pointer; user-select: none; }
.form__checkbox input { position: absolute; opacity: 0; cursor: pointer; height: 0; width: 0; }
.form__checkmark { top: -2px; left: 0; height: 16px; width: 16px; position: absolute; border: solid 2px #e6e6e6; background-color: #fff; transition: background-color .5s; }
.form__checkbox:hover input ~ .form__checkmark { background-color: #f3f3f3; }
.form__checkbox input:checked ~ .form__checkmark { background-color: #fe5c26; }
.form__checkbox input:checked ~ .form__checkmark:after { display: flex; }
</style>