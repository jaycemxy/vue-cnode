# vue-cnode

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

## components
- Header 头部
- PostList 帖子列表
- Article 文章详情页
- SlideBar 侧边栏
- UserInfo 用户个人信息页
- Pagination 底部分页组件

## 使用cnode提供的API
获取帖子列表：https://cnodejs.org/api/v1/topics（接收get参数）
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
