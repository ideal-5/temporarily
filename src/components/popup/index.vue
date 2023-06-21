
<!--
 * @SendWord:该组件向外传的参数
 * @keyboardSubmit  点击付款触发
 * @keyboardDelete  点击删除
 * @keyboardClickNumber 数字每改变一次 就会把新数组作为参数传递出去
 *
-->

<template>
    <div class="popup-box">
        <el-drawer title="我是标题" :visible.sync="drawer" :direction="'btt'">
            <span>我来啦!</span>
        </el-drawer>
    </div>
</template>

<script>

export default {
    data() {
        return {
            drawer: true
        }
    },
    alterDrawer() {
        this.drawer = !this.drawer
    }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
