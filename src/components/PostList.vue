<template>
  <div>
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif" title="加载中...">
    </div>
    <div v-else>
      <ul>
        <!-- 帖子头部 -->
        <li class="topic-header">
          <a class="topic-tab current-tab" href="#">全部</a>
          <a class="topic-tab" href="#">精华</a>
          <a class="topic-tab" href="#">分享</a>
          <a class="topic-tab" href="#">问答</a>
          <a class="topic-tab" href="#">招聘</a>
          <a class="topic-tab" href="#">客户端测试</a>
        </li>

        <!-- 帖子 -->
        <li class="clearfix" v-for="item in posts">
          <!-- 作者头像 -->
          <img :src="item.author.avatar_url" :title="item.author.loginname">

          <!-- 浏览量和回复量 -->
          <div class="replyandvisit">
            <span class="reply" title="回复数">{{ item.reply_count }}</span><span class="seperator">/</span><span class="visit" title="点击数">{{ item.visit_count }}</span>
          </div>

          <!-- 帖子分类 -->
          <span :class="[{'put_good': (item.good === true), 'put_top': (item.top === true), 'topiclist-tab': (item.good !== true && item.top !== true)}]">
            {{ item | tabFormatter }}
          </span>

          <!-- 帖子标题 -->
          <router-link :to="{name: 'post_content', params: {id: item.id}}">
            <a class="title" href="#">{{ item.title }}</a>
          </router-link>

          <!-- 最后回复时间 -->
          <a class="last_reply" href="#">
<!--            <img src="" alt="">-->
            <span>{{ item.last_reply_at | formatDate }}</span>
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: "PostList",
    data() {
      return {
        isLoading: false,
        posts: []
      }
    },
    beforeMount() {
      this.isLoading = true
      this.getData()
    },
    methods: {
      getData() {
        this.$http.get('https://cnodejs.org/api/v1/topics', {
          page: 1,
          limit: 20
        }).then((res) => {
          this.isLoading = false
          this.posts = res.data.data
        }).catch((err) => {
          console.log(err);
        })
      }
    }
  }
</script>

<style scoped>
  .clearfix::after {
    content: "";
    display: block;
    clear: both;
  }

  ul {
    background: #f5f5f5;
  }
  ul li {
    padding: 10px;
    border-top: 1px solid #f0f0f0;
    background: #fff;
  }
  ul li:nth-child(2) {
    border-top: none;
  }
  ul li:hover {
    background-color: #f5f5f5;
  }

  ul .topic-header {
    background: #f6f6f6;
    padding: 10px;
    border-radius: 3px 3px 0 0;
  }
  ul .topic-tab,
  ul .current-tab {
    margin: 0 10px;
    color: #80bd01;
    font-size: 14px;
  }
  ul .topic-tab:hover {
    color: #005580;
  }
  ul .current-tab {
    background: #80bd01;
    color: #fff;
    padding: 3px 4px;
    border-radius: 3px;
  }
  ul .current-tab:hover {
    color: #fff;
  }

  ul li img {
    width: 30px;
    float: left;
    cursor: pointer;
  }

  ul .replyandvisit {
    float: left;
    min-width: 70px;
    padding: 5px 0;
    /*line-height: 30px;*/
    text-align: center;
    /*margin-top: 8px;*/
  }
  ul .replyandvisit .reply {
    color: #9e78c0;
    font-size: 14px;
  }
  ul .replyandvisit .visit {
    color: #b4b4b4;
    font-size: 10px;
  }
  ul .seperator {
    text-align: center;
    margin: 0 1px;
  }

  /*ul .put_good, ul .put_top {*/
  /*  background: #80bd01;*/
  /*  padding: 2px 4px;*/
  /*  color: #fff;*/
  /*  font-size: 12px;*/
  /*  border-radius: 3px;*/
  /*}*/
  /*ul .topiclist-tab {*/
  /*  background-color: #e5e5e5;*/
  /*  color: #999;*/
  /*  padding: 2px 4px;*/
  /*  border-radius: 3px;*/
  /*  font-size: 12px;*/
  /*}*/

  ul .title {
    color: #333;
    max-width: 70%;
    white-space: nowrap;
    display: inline-block;
    font-size: 16px;
    line-height:30px;
    text-overflow: ellipsis;
    margin-left: 4px;
  }
  ul .title:hover {
    text-decoration: underline;
  }

  ul .last_reply {
    display: inline-block;
    height: 30px;
    line-height: 30px;
    float: right;
    min-width: 50px;
    color: #778087;
    font-size: 11px;
    text-align: right;
  }
</style>
