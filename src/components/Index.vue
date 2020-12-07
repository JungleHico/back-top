<template>
    <div class="page">
        <h1 class="header">BackTop  返回顶部组件</h1>
        <back-top :delay="1000"></back-top>
    </div>
</template>

<script>
import BackTop from './BackTop'

export default {
    components: {
        BackTop
    },
    data() {
        return {

        }
    }
}
</script>

<style scoped>
.page {
    height: 300vh;
}
.header {
    margin: 0;
}
</style>
