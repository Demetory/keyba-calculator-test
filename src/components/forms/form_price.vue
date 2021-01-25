<template>
    <div class="form__row">
        <p class="form__price">{{ label }} <span>{{ price }} ₽</span></p>
    </div>
</template>

<script>
export default {
    name: 'form_price',
    props : {
        label: {
            type: String,
            required: true,
            default: null
        },
        price: {
            type: Number,
            required: true,
            default: 0
        }
    }
}
</script>

<style scoped>
.form__row { margin-bottom: 20px; display: flex; width: 100%; }

.form__price { font-size: 14px; color: #000; }
.form__price span { font-size: 26px; color: #fe5c26; font-weight: 700; }
</style>