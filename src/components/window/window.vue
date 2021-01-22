<template>
    <div class="calc__window">
        <div class="calc__window-img">
            <div class="calc__window-col calc__window-left">
                <Button_Window :label="1" />
            </div>
            <div class="calc__window-col calc__window-right">
                <Button_Window :label="2" />
                <img alt="" src="@/assets/img/window-right-blind.png">
            </div>
        </div>
        <div class="calc__window-height"><p><span>1750 мм</span></p></div>
        <div class="calc__window-width"><p><span>1300 мм</span></p></div>
    </div>
</template>

<script>
import Button_Window from '@/components/buttons/window.button.vue'

export default {
    name : 'Window',
    components: { Button_Window }
}
</script>

<style scoped>
.calc__window { margin-bottom: 25px; display: flex; flex-wrap: wrap; }
.calc__window-left { display: flex; height: 100%; }
.calc__window-img { width: 289px; height: 280px; display: flex; background: url(../../assets/img/window-default.png) center center no-repeat; }
.calc__window-col { height: 100%; width: 50%; display: flex; align-items: center; justify-content: center; position: relative; }
.calc__window-col img { position: absolute; z-index: 0; }

.calc__window-width { margin-top: 28px; width: 289px; position: relative; }
.calc__window-width p { display: flex; align-items: center; justify-content: center; font-size: 12px; color: #898989; border-left: solid 1px #cccccc; border-right: solid 1px #cccccc; position: relative; }
.calc__window-width p span { padding: 0 5px; display: flex; background: #f3f3f3; z-index: 10; }
.calc__window-width p:after { top: 50%; left: 0; width: 100%; position: absolute; content: ''; border-top: 1px solid #ccc; z-index: 0; }

.calc__window-height { margin-left: 28px; height: 280px; position: relative; }
.calc__window-height p { writing-mode: vertical-lr; display: flex; width: 14px; height: 100%; align-items: center; justify-content: center; font-size: 12px; color: #898989; border-top: solid 1px #cccccc; border-bottom: solid 1px #cccccc; position: relative; line-height: 14px; }
.calc__window-height p span { padding: 5px; display: flex; background: #f3f3f3; z-index: 10; align-items: center; justify-content: center; }
.calc__window-height p:after { top: 0; left: 50%; height: 100%; position: absolute; content: ''; width: 1px; background-color: #ccc; z-index: 0; }

@media screen and (max-width: 780px){
    .calc__window-height { margin-right: 25px; }
}

@media screen and (max-width: 600px){
    .calc__window-height { margin-right: 0; }
}
</style>