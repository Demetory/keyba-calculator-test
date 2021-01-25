<template>
    <div class="footer" v-if="data">
        <p v-for="paragraph in data" :key="paragraph.id">{{ paragraph }}</p>
    </div>
</template>

<script>
export default {
    name : 'form_footer',
    props : {
        data : {
            type: Array,
            required: true,
            default: null
        }
    }
}
</script>

<style scoped>
.footer { padding: 0 28px; }
.footer p { font-size: 13px; line-height: 18px; color: #707070; }
</style>