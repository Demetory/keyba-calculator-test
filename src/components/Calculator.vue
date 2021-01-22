<template>
    <div class="calc__body">
        <div class="calc__body-l">
            <Window />
            <div class="calc__params">
                <div class="calc__params-row">
                    <Button_Window :label="1" />
                    <Dropdown :className="'calc__dropdown-short'" />
                </div><!-- .calc__params-row //-->
                <div class="calc__params-row">
                    <Button_Window :label="2" />
                    <Dropdown :className="'calc__dropdown-short'" />
                </div><!-- .calc__params-row //-->
                <div class="calc__params-row">
                    <p class="calc__params-mosquito">
                        <Checkbox />
                    </p>
                </div><!-- .calc__params-row //-->
            </div><!-- .calc__params //-->
        </div><!-- .calc__body-l //-->
        <div class="calc__body-r">
            <h2 class="calc__title">{{ states.text.title }}</h2>
            <div class="calc__params-row">
                <div class="calc__params-col">
                    <Text :data="['param-width', 'Ширина']" />
                </div>
                <div class="calc__params-col">
                    <Text :data="['param-height', 'Длина']"/>
                </div>
            </div><!-- .calc__params-row //-->
            <div class="calc__params-row">
                <Dropdown :label="'ПВХ-профиль'" />
            </div><!-- .calc__params-row //-->
            <div class="calc__params-row">
                <Dropdown :label="'Стеклопакет'" />
            </div><!-- .calc__params-row //-->
            <div class="calc__params-row">
                <Dropdown :label="'Цвет'" />
            </div><!-- .calc__params-row //-->
            <div class="calc__params-row">
                <p class="calc__params-price">{{ states.text.price }} <span>50 190 ₽</span></p>
            </div><!-- .calc__params-row //-->
            <div class="calc__params-row">
                <Button_Cart :label="states.text.cart" />
            </div><!-- .calc__params-row //-->
        </div><!-- .calc__body-r //-->
    </div><!-- .calc__body //-->
    <Footer :data="states.text.footer" />
</template>

<script>
import states from '@/assets/data/options.json'

import Footer from '@/components/footer/footer.vue'
import Button_Cart from '@/components/buttons/cart.button.vue'
import Button_Window from '@/components/buttons/window.button.vue'
import Window from '@/components/window/window.vue'
import Dropdown from '@/components/selectors/input.dropdown.vue'
import Checkbox from '@/components/selectors/input.checkbox.vue'
import Text from '@/components/selectors/input.text.vue'

export default {
    name: 'Calculator',
    components: { Dropdown, Checkbox, Text, Window, Button_Cart, Button_Window, Footer },
    data() {
        return { states }
    },
    computed: {
        get_data(){
            return states.params.map((selector) => {
                return selector
            })
        }
    },
    methods : {

    },
    mounted() {
        console.log(states);
    }
}
</script>

<style scoped>
.calc__body { padding: 53px 28px 37px; display: flex; }
.calc__body-l { padding-left: 56px; flex: 1; }
.calc__body-r { padding: 0 20px; min-width: 225px; }

.calc__params-row { margin-bottom: 20px; display: flex; flex: 1; flex-wrap: wrap; align-items: center; }
.calc__params-col { margin: 0 8px; flex-direction: column; flex: 1 1 auto; }
.calc__params-col:first-child { margin-left: 0; }
.calc__params-col:last-child { margin-right: 0; }

.calc__title { margin: 0 0 32px 0; padding: 0; font-size: 20px; font-weight: 700; line-height: 24px; color: #fe5c26; }

.calc__params-mosquito { display: flex; font-size: 13px; color: #707070; align-items: center; }

.calc__params-price { font-size: 14px; color: #000; }
.calc__params-price span { font-size: 26px; color: #fe5c26; font-weight: 700; }

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