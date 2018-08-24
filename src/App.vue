<template>
  <div id="app">
    <Header></Header>  <!-- 组件使用第三步：放在合适的加载位置 -->
    <div class="main">
      <post-list></post-list>
    </div>
  </div>
</template>

<script>
import Header from './components/Header'  // 组件使用第一步：引入
import PostList from './components/PostList'

export default {
  name: 'App',
  components: {  // 组件使用第二步：注册
    Header,
    PostList
  }
}
</script>

<style>
  .main {
    width: 80%;
    margin: 0 auto;
  }
</style>
