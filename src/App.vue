<template>
  <div id="app">
    <Header></Header>   <!-- 组件使用第三步：放在合适的加载位置 -->
  </div>
</template>

<script>
import Header from './components/Header'  // 组件使用第一步：引入
export default {
  name: 'App',
  components: {  // 组件使用第二步：注册
    Header
  }
}
</script>

<style>

</style>
