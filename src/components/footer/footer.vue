<template>
    <div class="calc__foot" v-if="data">
        <p v-for="paragraph in data" :key="paragraph.id">{{ paragraph }}</p>
    </div>
</template>

<script>
export default {
    name : 'Footer',
    props : ['data']
}
</script>

<style scoped>
.calc__foot { padding: 0 28px; }
.calc__foot p { font-size: 13px; line-height: 18px; color: #707070; }
</style>