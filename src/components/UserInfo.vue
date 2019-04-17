<template>
  <div>
    <div class="userInfo">
      <!-- loading -->
      <div class="loading" v-if="isLoading">
        <img src="../assets/loading.gif" title="加载中...">
      </div>

      <!-- 用户信息-->
      <div class="" v-else>

        <!-- 主页 -->
        <div class="panel">

          <!-- 主页 header -->
          <div class="header">
            <a href="#">主页</a> <i>/</i>
          </div>

          <!-- 主页 main -->
          <div class="main">
            <img class="big-headImg" :src="userInfo.avatar_url" :title="userInfo.loginname">
            <span class="userName">{{ userInfo.loginname }}</span>
            <div class="user_profile">
              <p>{{ userInfo.score }}积分</p>
              <p class="github">
                <svg-icon icon-class="github" />
                <a href="#">@{{ userInfo.loginname }}</a>
              </p>
              <p class="col_fade">注册时间 {{ userInfo.create_at | formatDate }}</p>
            </div>
          </div>

        </div>

        <!-- 最近创建的话题 -->
        <div class="panel">

          <!-- 最近创建的话题 header -->
          <div class="header">
            <span>最近创建的话题</span>
          </div>

          <!-- 最近创建的话题 cell -->
          <div class="main cell">
            <ul>
              <li v-for="item in userInfo.recent_topics">
                <img class="middle-headImg" :src="userInfo.avatar_url" :title="userInfo.loginname">
                <router-link :to="{
                  name: 'post_content',
                  params: {
                    id: item.id
                  }
                }">
                  <a href="#" class="title" :title="item.title">{{ item.title }}</a>
                </router-link>
                <div class="reply">
                  <img class="small-headImg" :src="userInfo.avatar_url" alt="">
                  <span class="">{{ userInfo.recent_topics[0].last_reply_at | formatDate}}</span>
                </div>
              </li>
              <li>
                <a class="more" href="#">查看更多 >></a>
              </li>
            </ul>
<!--            <div class="">-->
<!--              <img class="middle-headImg" :src="userInfo.avatar_url" :title="userInfo.loginname">-->
<!--              <span class="">-->
<!--                <span>{{ userInfo.recent_replies.length }}</span> / <span>{{ userInfo.recent_replies.length }}</span>-->
<!--              </span>-->
<!--              <a class="" href="#">{{ userInfo.recent_topics[0].title }}积分</a>-->
<!--              <span class="">{{ userInfo.recent_topics[0].last_reply_at | formatDate}}</span>-->
<!--              <img class="small-headImg" :src="userInfo.avatar_url" alt="">-->
<!--            </div>-->
<!--            <div class="">-->
<!--              <a href="#">查看更多 >></a>-->
<!--            </div>-->
          </div>

        </div>

        <!-- 最近参与的话题 -->
        <div class="panel">

          <!-- 最近参与的话题 header-->
          <div class="header">
            <span>最近参与的话题</span>
          </div>

          <!-- 最近参与的话题 cell -->
          <div class="main cell">
            <ul>
              <li v-for="item in userInfo.recent_replies">
                <img class="middle-headImg" :src="item.author.avatar_url" :title="item.author.loginname">
                <router-link :to="{
                  name: 'post_content',
                  params: {
                    id: item.id
                  }
                }">
                  <a href="#" class="title" :title="item.title">{{ item.title }}</a>
                </router-link>
                <div class="reply">
                  <img class="small-headImg" :src="item.author.avatar_url" alt="">
                  <span class="">{{ item.last_reply_at | formatDate}}</span>
                </div>
              </li>
              <li>
                <a class="more" href="#">查看更多 >></a>
              </li>
            </ul>
          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "UserInfo",
    components: {
    },
    data() {
      return {
        isLoading: false,
        userInfo: {}
      }
    },
    methods: {
      getUserInfoData() {
        this.$http.get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
          .then((res) => {
            this.isLoading = false
            if (res.data.success === true) {
              this.userInfo = res.data.data
            }
            console.log(res.data.data)
          })
          .catch((err) => {
            console.log(err)
          })
      }
    },
    beforeMount() {
      this.isLoading = true
      this.getUserInfoData()
    }
  }
</script>

<style scoped>
  .panel {
    margin-bottom: 13px;
    font-size: 14px;
    word-break: break-word;
    border-radius: 3px;
  }
  .panel .header {
    padding: 10px;
    background-color: #f6f6f6;
  }
  .header a {
    color: #80bd01;
  }
  .header a:hover {
    text-decoration: underline;
  }
  .header i {
    padding: 0 5px;
    display: inline-block;
    color: #ccc;
    font-style: normal;
  }
  .header span {
    color: #444;
  }
  .panel .main {
    padding: 10px;
    border-top: 1px solid #e5e5e5;
    background-color: #fff;
    margin: 0;
    width: 100%;
    line-height: 2em;
  }
  .panel .cell {
    padding: 0;
  }
  .main .big-headImg {
    width: 40px;
    height: 40px;
  }
  .main .middle-headImg {
    width: 30px;
    height: 30px;
  }
  .main .small-headImg {
    width: 18px;
    height: 18px;
    margin-right: 0.5em;
  }
  .main .userName {
    color: #778087;
    text-overflow: ellipsis;
    overflow: hidden;
    vertical-align: top;
    margin-left: 8px;
  }
  .main .github svg {
    color: #000;
    opacity: .4;
    margin-left: 4px;
  }
  .main .github svg:hover {
    opacity: .8;
  }
  .main .github a {
    color: #778087;
    margin-left: 4px;
  }
  .main .col_fade {
    color: #ababab;
    margin-bottom: 10px;
  }
  .main ul {
  }
  .cell li {
    padding: 10px;
    border-bottom: 1px solid #f0f0f0;
  }
  .cell li:last-child {
    border-bottom: none;
    padding-top: 7px;
    padding-bottom: 7px;
  }
  .cell .reply {
    float: right;
  }
  .cell .title {
    max-width: 70%;
    white-space: nowrap;
    display: inline-block;
    vertical-align: middle;
    font-size: 16px;
    line-height: 30px;
    margin-left: 70px;
    color: #08c;
  }
  .cell .title:hover {
    text-decoration: underline;
  }
  .cell .more {
    color: #666;
  }
  .cell .more:hover {
    color: #385f8a;
  }

</style>
