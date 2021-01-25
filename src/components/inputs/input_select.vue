<template>
<div :class="get_class(name)">
    <p v-if="label" :class="get_label(name)">{{ label }}</p>
    <div class="select" :tabindex="tabindex" @blur="open = false">
        <div class="select__top" :class="{ open: open }" @click="open = !open">{{ selected.text }} <i class="select__arrow" :class="{ up: open }" /></div>
        <div class="select__dropdown" :class="{ hidden: !open }">
            <div class="select__item" v-for="(option, i) of options"
                :key="i"
                @click="selected = option; open = false; $emit('input', option); "
            >
                <i v-if="option.icon" class="icon" :class="option.icon"></i>
                {{ option.text }}
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'input_select',
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
        options: {
            type: Array,
            required: true
        },
        default: {
            type: Object,
            required: false,
            default: null
        },
        tabindex: {
            type: Number,
            required: false,
            default: 0
        }
    },
    data() {
        return {
            selected: this.default
                ? this.default
                : this.options.length > 0
                ? this.options[0]
                : null,
            open: false
        }
    },
    methods : {
        get_class(name){
            if (/window/.test(name) === true){ return 'row-flex' }
            else { return 'row' }
        },
        get_label(name){
            if (/window/.test(name) === true){ return 'select__label-window' }
            else { return 'select__label' }
        }
    },
    mounted() {
        this.$emit("input", this.selected);
    }
}
</script>

<style scoped>
.row { width: 100%; }
.row-flex { display: flex; align-items: center; flex: 1; }
.select__label { display: block; width: 100%; padding-bottom: 10px; color: #19191a; font-size: 14px; }
.select__label-window { margin-right: 14px; border-radius: 50%; width: 44px; height: 44px; display: flex; align-items: center; justify-content: center; cursor: default; background-color: #e6e6e6; font-size: 30px; font-weight: 700; color: #fff; }

.select__arrow { margin-left: auto; padding: 3px; display: inline-block; border: solid #494949; border-width: 0 1px 1px 0; transform: rotate(45deg); transition: all .5s; }

.select { display: flex; width: 100%; max-width: 225px; position: relative; outline: none; }
.select__top { padding: 10px 20px; display: flex; flex: 1; max-height: 36px; background-color: #fff; color: #707070; font-size: 14px; cursor: pointer; user-select: none; align-items: center; }
.select__dropdown { top: 100%; left: 0; right: 0; flex: 1; display: flex; flex-direction: column; position: absolute; overflow: hidden; z-index: 1; background-color: #fff; box-shadow: 0px 15px 15px rgba(125, 125, 125, .1); }
.select__item { padding: 10px 20px; display: flex; flex: 1; font-size: 14px; color: #707070; cursor: pointer; user-select: none; transition: background-color .5s, color .5s; align-items: center; }
.select__item:hover { background-color: #f9f9fa; color: #fe5c26; }

.hidden { display: none; }
.up { transform: rotate(-135deg); }
.icon { margin-right: 14px; width: 19px; height: 19px; display: flex; }
.white { background: url(../../assets/img/dropdown-point-white.png) center center no-repeat; }
.color { background: url(../../assets/img/dropdown-point-color.png) center center no-repeat; }
</style>