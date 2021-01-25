<template>
<div id="calculator">
    <div class="calc__body">
        <div class="calc__body-l">
            <Window :window_width="get_width()" :window_height="get_height()" />
            <form_window :inputs="form_window_inputs" v-model="formData" />
        </div>
        <div class="calc__body-r">
            <h2 class="form__title">{{ states.form_params.str_title }}</h2>
            <form_params :inputs="form_params_inputs" v-model="formData" />
            <form_price :label="states.form_params.str_price" :price="formData.price" />
            <cart_button :label="states.form_params.str_cart" :cart="formData" />
        </div>
    </div>
    <form_footer :data="states.form_params.arr_footer" />
</div>
</template>

<script>
import states from '@/assets/data/options.json'

import form_window from '@/components/forms/form_window.vue'
import form_params from '@/components/forms/form_params.vue'
import form_price from '@/components/forms/form_price.vue'
import cart_button from '@/components/buttons/cart.button.vue'
import form_footer from '@/components/footer/footer.vue'

import Window from '@/components/window/window.vue'

export default {
    name: 'Calculator',
    components: { form_window, form_params, form_price, cart_button, form_footer, Window },
    data: () => ({
        states,
        formData : { new_price: [], price : 0 },
        form_params_inputs : {},
        form_window_inputs : {},
    }),
    methods: {
        get_width(){
            if (this.formData.param_width){ return Number.parseInt(this.formData.param_width.value) }
        },
        get_height(){
            if (this.formData.param_height){ return Number.parseInt(this.formData.param_height.value) }
        }
    },
    mounted() {
        this.form_params_inputs = states.form_params.inputs.map((inputs) => { return inputs })
        this.form_window_inputs = states.form_window.inputs.map((inputs) => { return inputs })

        this.get_width();
        this.get_height();
    }
}
</script>

<style scoped>
#calculator { margin: 0 auto; padding: 0 0 40px 0; max-width: 794px; display: flex; flex-direction: column; background-color: #f3f3f3; text-align: left; }

.calc__body { padding: 53px 28px 37px; display: flex; }
.calc__body-l { padding-left: 56px; flex: 1; }
.calc__body-r { padding: 0 20px; min-width: 225px; }

.form__title { margin: 0 0 32px 0; padding: 0; font-size: 20px; font-weight: 700; line-height: 24px; color: #fe5c26; }


@media screen and (max-width: 840px){
    .calc__body-l { padding-left: 28px; }
}

@media screen and (max-width: 780px){
    .calc__body { flex-wrap: wrap; }
    .calc__body-l { min-width: 100%; padding-left: 0px; flex: 0; }
    .calc__body-r { margin-top: 28px; padding: 0; min-width: 100%; flex: 0; }
}

@media screen and (max-width: 440px){
    .calc__body { padding: 15px; }
}
</style>