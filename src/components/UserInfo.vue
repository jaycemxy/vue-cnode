<template>
  <div class="UserInfo">
    <!-- 数据未返回时，显示正在加载的动画 -->
    <div class="loading" v-if="isLoading">
        <img src="../assets/loading.gif">
    </div>
    <div class="userInfomation">
        <section>
            <img :src="userinfo.avatar_url">
            <span>{{ userinfo.loginname }}</span>
            <p>{{ userinfo.score }}积分</p>
            <p>注册时间{{ userinfo.create_at | formatDate }}</p>
        </section>
        <div class="replies">
            <p>回复的主题</p>
            <ul>
                <li v-for="item in userinfo.recent_replies">
                    <router-link :to="{
                        name: 'post_content',
                        params:{
                            id: item.id
                        }
                    }">
                        {{ item.title }}
                    </router-link>
                </li>
            </ul>
        </div>
        <div class="topics">
            <p>创建的主题</p>
            <ul>
                <li v-for="item in userinfo.recent_topics">
                    <router-link :to="{
                        name: 'post_content',
                        params:{
                            id: item.id
                        }
                    }">
                        {{ item.title }}
                    </router-link>
                </li>
            </ul>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserInfo',
  data(){
      return {
          isLoading: false,
          userinfo: {}
      }
  },
  methods: {
        getUserData() {
        this.$http
            .get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
            .then(res => {
            this.isLoading = false; // 数据加载成功取消loading动画
            this.userinfo = res.data.data;
            console.log(res);
            })
            .catch(function(err) {
            // 处理返回失败
            console.log(err);
            });
        }
    },
    beforeMount() {
        this.isLoading = true; // 加载成功前显示loading动画
        this.getUserData(); // 加载成功后显示数据
    }
}
</script>

<style scoped>
    .userInfomation {
        background: white;
        width: 75%;
        margin: 10px auto;
    }
    .userInfomation section {
        padding: 12px;
    }
    .userInfomation img {
        width: 30px;
    }
    .userInfomation li {
        list-style:none;
    }
    .userInfomation .replies,
    .userInfomation .topics {
        font-size: 0.72rem;
        border-top: 10px #DDDDDD solid;
    }
    .userInfomation > div > p {
        padding: 12px 0 12px 12px;
        background-color: rgba(212, 205, 205, 0.17);
        font-size: 0.75rem;
        margin: 0;
    }
    .userInfomation > div >ul > li {
        padding: 4px 0 4px 12px;
        white-space: nowrap;
        font-size: 0.72rem;
        text-overflow: ellipsis;
        overflow: hidden;
        line-height: 30px;
        vertical-align: middle;
    }
    .userInfomation > div >ul > li > a {
        color: #094E99;
        text-decoration: none;
    }
</style>
