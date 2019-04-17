<template>
  <div class="SlideBar">
    <!-- 个人信息 -->
    <div class="panel userInfo">
      <div class="header">作者</div>
      <div class="main">
        <router-link :to="{
          name: 'userinfo',
          params: {
            name: userInfo.loginname
          }
        }">
          <img class="head-img" :src="userInfo.avatar_url" :title="userInfo.loginname">
        </router-link>
        <span class="userName">{{ userInfo.loginname }}</span>
        <p class="score">积分：{{ userInfo.score }}</p>
      </div>
    </div>

    <!-- 广告 -->
    <div class="ad main">
      <img src="../assets/ad1.jpg" alt="">
      <img src="../assets/ad2.jpg" alt="">
      <img src="../assets/ad3.jpg" alt="">
      <img src="../assets/ad4.jpg" alt="">
    </div>

    <!-- 作者最近主题 -->
    <div class="panel friendly">
      <div class="header">作者最近主题</div>
      <div class="main">
        <ul>
            <li v-for="item in topicLimit" :title="item.title">
              <router-link :to="{
                name: 'post_content',
                params: {
                  id: item.id,
                  name: item.author.loginname
                }
              }">
                <a href="#">{{ item.title }}</a>
              </router-link>
            </li>
        </ul>
      </div>

    </div>

    <!-- 作者最近回复 -->
    <div class="panel erweima">
      <div class="header">作者最近回复</div>
      <div class="main">
        <ul>
          <li v-for="item in replyLimit" :title="item.title">
            <router-link :to="{
              name: 'post_content',
              params: {
                id: item.id,
                name: item.author.loginname
              }
            }">
              <a href="#">{{ item.title }}</a>
            </router-link>
          </li>
        </ul>
      </div>

    </div>

  </div>
</template>

<script>
  export default {
    name: "SlideBar",
    data() {
      return {
        userInfo: {}
      }
    },
    methods: {
      getUserInfoData() {
        this.$http.get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
          .then((res) => {
            if (res.data.success === true) {
              this.userInfo = res.data.data
            }
          })
          .catch((err) => {
            console.log(err);
          })
      }
    },
    computed: {
      topicLimit() {
        if (this.userInfo.recent_topics) {
          return this.userInfo.recent_topics.slice(0, 5)
        }
      },
      replyLimit() {
        if (this.userInfo.recent_replies) {
          return this.userInfo.recent_replies.slice(0, 5)
        }
      }
    },
    beforeMount() {
      this.getUserInfoData()
    }
  }
</script>

<style scoped>
  .SlideBar {
    width: 290px;
    float: right;
  }

  .panel {
    margin-bottom: 13px;
    font-size: 14px;
    word-break: break-word;
    border-radius: 3px;
  }
  .main {
    padding: 10px;
    border-top: 1px solid #e5e5e5;
    background-color: #fff;
    margin: 0;
    width: 100%;
    line-height: 2em;
    color: #778087;
  }
  .panel .header {
    padding: 10px;
    background-color: #f6f6f6;
  }

  .main .head-img {
    width: 48px;
    height: 48px;
  }
  .main .userName {
    vertical-align: top;
    font-size: 16px;
    margin-top: 10px;
    display: inline-block;
  }
  .main .score {
    color: #333;
  }
  .ad {
    margin-bottom: 13px;
  }
  .ad img {
    width: 270px;
  }
  .main ul li {
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }
  .main ul li a {
    color: #778087;
  }

</style>
