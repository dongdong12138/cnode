<template>
  <div id="app">
    <Header></Header>
    <div class="main">
      <router-view name="main"></router-view>
    </div>
  </div>
</template>

<script>
  import Header from './components/Header'
  import PostList from './components/PostList'
  import UserInfo from './components/UserInfo'
export default {
  name: 'App',
  components: {
    Header,
    PostList,
    UserInfo
  }
}
</script>

<style>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #333;
  height: 2000px;

}
  * {
    margin: 0; padding: 0;
    box-sizing: border-box;
  }
  body {
    background: #e1e1e1;
    word-break: break-word;
  }
  ul, li {
    list-style: none;
  }
  a {
    text-decoration: none;
    color: rgb(204, 204, 204);
  }
  form, input {
    border: none;
    outline: none;
  }

  .main {
    width: 90%;
    max-width: 1400px;
    /*min-width: 960px;*/
    margin: 15px auto;
  }

.put_good, .put_top {
  background: #80bd01;
  padding: 2px 4px;
  color: #fff;
  font-size: 12px;
  border-radius: 3px;
}
.topiclist-tab {
  background-color: #e5e5e5;
  color: #999;
  padding: 2px 4px;
  border-radius: 3px;
  font-size: 12px;
}


</style>
