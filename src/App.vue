<template>
  <div id="app">
    <Header></Header>  <!-- 组件使用第三步：放在合适的加载位置 -->
    <div class="main">
      <router-view name="slidebar"></router-view>
      <router-view name="main"></router-view>
    </div>
  </div>
</template>

<script>
import Header from './components/Header'  // 组件使用第一步：引入
import PostList from './components/PostList'
import Article from './components/Article'

export default {
  name: 'App',
  components: {  // 组件使用第二步：注册
    Header,
    PostList,
    Article
  }
}
</script>

<style>
  #app{
    background: #dddddd;
  }
  .main {
    width: 80%;
    margin: 0 auto;
  }
</style>
