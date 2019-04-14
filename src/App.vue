<template>
  <div id="app">
    <Header></Header>
    <div class="main">
      <PostList></PostList>
    </div>
  </div>
</template>

<script>
  import Header from './components/Header'
  import PostList from './components/PostList'
export default {
  name: 'App',
  components: {
    Header,
    PostList
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


</style>
