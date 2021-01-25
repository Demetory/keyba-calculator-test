<template>
    <p v-if="label" class="calc__input-label">{{ label }}</p>
    <ul :className="className + ' calc__dropdown'">
        <li>{{ data.options[0].label }} <span class="calc__dropdown-arrow"><img alt="" src="@/assets/img/dropdown-arrow-down.png"></span>
            <ul v-for = "option in data.options" :key = "option.id">
                <li data-price="{{ option.price }}" data-id="">{{ option.label }}</li>
            </ul>
        </li>
    </ul>
</template>

<script>
export default {
    name : 'Dropdown',
    props : ['data', 'label', 'className']
}
</script>

<style scoped>
.calc__input-label { display: block; width: 100%; padding-bottom: 10px; color: #19191a; font-size: 14px; }

.calc__dropdown { display: flex; width: 100%; position: relative; }
.calc__dropdown-short { margin-left: 14px; max-width: 204px; }
.calc__dropdown li { padding: 10px 20px; display: flex; flex: 1; font-size: 14px; background-color: #fff; color: #707070; cursor: pointer; align-items: center; transition: background-color .5s, color .5s; max-height: 36px; position: relative; }
.calc__dropdown li span { display: flex; align-items: center; }
.calc__dropdown li span.calc__dropdown-icon { margin-right: 14px; }
.calc__dropdown li span.calc__dropdown-arrow { margin-left: auto; }
.calc__dropdown ul { top: 100%; left: 0; width: 100%; display: none; position: absolute; flex-direction: column; }
.calc__dropdown li:hover > ul { display: flex; box-shadow: 0px 15px 15px rgba(125, 125, 125, .1); position: absolute; z-index: 999999999; border-top: solid 1px #ccc; }
.calc__dropdown ul li:hover { background-color: #f9f9fa; color: #fe5c26; }
</style>