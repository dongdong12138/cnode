<template>
  <div class="article">
    <!-- loading -->
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif" title="加载中...">
    </div>

    <!-- 帖子详情 -->
    <div v-else>
      <!-- 帖子头部 -->
      <div class="topic_header">
        <div class="topic_title">
          <span class="put_top">{{ post | tabFormatter }}</span>
          {{ post.title }}
        </div>
        <div class="changes">
          <span>• 发布于 {{ post.create_at | formatDate }}</span>
          <span>• 作者 <span class="author_name">{{ post.author.loginname }}</span></span>
          <span>• {{ post.visit_count }} 次浏览</span>
          <span>• 来自 {{ post | tabFormatter }}</span>
        </div>
      </div>

      <!-- 帖子内容 -->
      <div class="topic_content" v-html="post.content"></div>

      <!-- 回复 -->
      <div class="reply">
        <div class="topbar">{{ post.reply_count }} 回复</div>
        <ul>
          <li class="replySec" v-for="(reply, index) in post.replies">
            <div class="replyUp">
              <router-link :to="{name: 'userinfo', params: {name: reply.author.loginname}}">
                <img :src="reply.author.avatar_url" alt="">
              </router-link>
              <router-link :to="{name: 'userinfo', params: {name: reply.author.loginname}}">
                <a class="dark" href="#">{{ reply.author.loginname }}</a>
              </router-link>
              <a class="reply_time" href="#">{{ index+1 }}楼•{{ reply.create_at | formatDate }}</a>
              <div class="up-count">
                <svg-icon icon-class="zan" />
                <a class="">{{ reply.ups.length }}</a>
              </div>
            </div>
            <div class="reply_content">
              <p v-html="reply.content"></p>
            </div>

          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Article",
    data() {
      return {
        isLoading: false,
        post: {}
      }
    },
    methods: {
      getArticleData() {
        this.$http.get(`https://cnodejs.org/api/v1/topic/${this.$route.params.id}`)
          .then((res) => {
            this.isLoading = false
            if (res.data.success === true) {
              this.post = res.data.data
            }
          })
          .catch((err) => {
            console.log(err)
          })
      }
    },
    beforeMount() {
      this.isLoading = true
      this.getArticleData()
    },
    watch: {
      '$route'(to, from) {
        this.getArticleData()
      }
    }

  }
</script>

<style>
  /*@import url("../assets/font_1142107_iv2cstinr2/iconfont.css");*/
  @import url('../assets/markdown-github.css');
  .markdown-text img {
    width: 92% !important;
  }
  .markdown-text p,
  .preview p {
    white-space: pre-wrap;
    word-wrap: break-word;
    line-height: 2em;
    margin: 1em 0;
  }
  .markdown-text>:last-child,
  .preview>:last-child,
  textarea#title {
    margin-bottom: 1em;
  }
  .markdown-text a {
    color: #08c;
  }
  .markdown-text>:first-child, .preview>:first-child {
    margin-top: 0;
  }

  .icon {
    width: 1em; height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
  }

  .article {
    /*float: left;*/
    margin-right: 305px;
    min-width: 655px;
  }
  .topic_header {
    /*border: 1px solid red;*/
    background-color: #fff;
    padding: 10px;
    border-radius: 3px 3px 0 0;
  }
  .topic_header .topic_title {
    font-size: 22px;
    font-weight: 700;
    margin: 8px 0;
    display: inline-block;
    vertical-align: bottom;
    width: 75%;
    line-height: 130%;
  }
  .topic_header .changes {
    font-size: 12px;
    color: #838383;
  }
  .changes .author_name {
    cursor: pointer;
  }
  .changes .author_name:hover {
    text-decoration: underline;
  }


  .topic_content {
    /*border: 1px solid red;*/
    padding: 10px;
    border-top: 1px solid #e5e5e5;
    border-radius: 0 0 3px 3px;
    background-color: #fff;
    line-height: 2em;
  }
  .topic_content img {
    cursor: pointer;
    height: auto;
    max-width: 100%;
    vertical-align: middle;
    border: 0;
  }
  .topic_content p {
    font-size: 15px;
    line-height: 1.7em;
    overflow: auto;
    margin: 1em 0;
    word-break: break-word;
  }
  .topic_content a:hover {
    text-decoration: underline;
  }


  .reply {
    /*border: 1px solid red;*/
    margin: 13px 0;
  }
  .reply .topbar {
    padding: 10px;
    background-color: #f6f6f6;
    border-radius: 3px 3px 0 0;
    color: #444;
    line-height: 20px;
    font-size: 14px;
    word-break: break-word;

  }
  .reply .replySec {
    position: relative;
    padding: 10px;
    font-size: 14px;
    background: #fff;
    border-top: 1px solid #f0f0f0;
    overflow: hidden;
    word-break: break-word;

  }
  .reply .replyUp {
    font-size: 14px;
  }
  .replyUp img {
    width: 30px;
    height: 30px;
    border-radius: 3px;
    max-width: 100%;
    vertical-align: middle;
    border: 0;
  }
  .replyUp .dark {
    color: #666;
    text-decoration: none;
    text-overflow: ellipsis;
    font-size: 12px;
    font-weight: 700;
    margin-left: 10px;
  }
  .replyUp .dark:hover {
    color: #385f8a;
  }
  .replyUp .reply_time {
    font-size: 11px;
    color: #08c;
    text-decoration: none;
    
  }
  .replyUp .reply_time:hover {
    text-decoration: underline;
  }
  .reply .up-count {
    float: right;
    margin-left: 20px;
    font-size: 15px;
  }
  .reply .up-count a {
    color: gray;
  }
  .reply svg {
    cursor: pointer;
    color: #000;
    opacity: .8;
  }
  .reply svg:hover {
    color: #000;
    opacity: 1;
  }
  .reply .reply_content {
    padding-left: 50px;
    color: #333;
    font-size: 14px;

  }
  .reply_content p {
    font-size: 15px;
    line-height: 1.7em;
    overflow: auto;
  }


</style>
