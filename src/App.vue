<template>
  <div id="app">
    <div style="height:60px;line-height:60px;font-size:30px;width:100%;text-align:center">父母圈</div>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style lang="less">
@import '~vux/src/styles/reset.less';

body {
  background-color: #fbf9fe;
}
</style>
