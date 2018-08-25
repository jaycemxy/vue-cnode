## vue-cli脚手架搭建项目
在博客中有总结：https://jaycemxy.github.io/2018/08/23/vue-cli%E8%84%9A%E6%89%8B%E6%9E%B6%E6%90%AD%E5%BB%BA%E9%A1%B9%E7%9B%AE/

## components
- Header 头部
- PostList 帖子列表
- Article 文章详情页
- SlideBar 侧边栏
- UserInfo 用户个人信息页
- Pagination 底部分页组件

## 使用cnode提供的API
### 获取帖子列表
API： https://cnodejs.org/api/v1/topics（接收get参数）
- page 页数
- limit 每页显示帖子数量

获得的参数分析（推荐HiJson字符串格式化工具，帮助查看json数据）
- 头像：author.avatar_url
- 回复量/浏览量：reply_count/visit_count
- 帖子标题：title
- 需要使用过滤器：
  - 时间：last_reply_at
  - 帖子分类：
    - top：置顶
    - good：精华
    - tab：其他
      - share：分享
      - ask：问答
      - job：招聘
### 获取帖子详情页
API：https://cnodejs.org/api/v1/topic/+帖子ID
### 获取用户详情页
API：https://cnodejs.org/api/v1/user/+username
## 使用axios发送请求
1、安装
```
npm install axios
```

2、在main.js文件下引入
```
import Axios from 'axios'
```

3、将axios全局挂载到Vue原型上
```
Vue.prototype.$http = Axios;  // 这样就可以直接使用this.$http发送请求
```

更多请看我的一篇博客总结：https://jaycemxy.github.io/2018/08/23/axios%E7%9A%84%E4%BD%BF%E7%94%A8/
## 监听路由变化
当你从页面：
```
http://localhost:8080/#/topic/5a9661ff71327bb413bbff5b&author=nswbmw
```

跳转到页面：
```
http://localhost:8080/#/userinfo/nswbmw
```

可以明显看出路由的变化，从topic到userinfo，并且我们在index.js文件中也定义了两个路由跳转的路径
```
{
  name: 'post_content',
  path: '/topic/:id&author=:name',
  components: {
    main: Article,
    slidebar: SlideBar
  }
},
{
  name: 'user_info',
  path: '/userinfo/:name',
  components: {
    main: UserInfo
  }
}
```

但当你从：
```
http://localhost:8080/#/topic/5a9661ff71327bb413bbff5b&author=nswbmw
```

转向页面：
```
http://localhost:8080/#/topic/5a99733f8edf56a344936fda&author=nswbmw
```

这里仔细观察topic未发生变化，但却是不同的话题页面，这时我们需要用到vue提供给我们的watch对象，它可以监听路由发生的改变
```
// Article.vue中
watch: {
  '$route'(to, from){
      this.getArticleData();
  }
}
```
