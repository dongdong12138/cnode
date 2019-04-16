<template>
  <div class="header">
    <div class="container">
      <router-link :to="{name: 'root'}">
        <img src="../assets/cnodejs_light.svg" alt="logo">
      </router-link>
      <form action="">
        <input type="search">
      </form>
      <ul>
        <li><a href="#">首页</a></li>
        <li><a href="#">新手入门</a></li>
        <li><a href="#">API</a></li>
        <li><a href="#">关于</a></li>
        <li><a href="#">注册</a></li>
        <li><a href="#">登录</a></li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Header",
  }
</script>

<style scoped>
  .header {
    background-color: #444;
  }
  .container {
    height: 50px;
    max-width: 1400px;
    min-width: 960px;
    margin: 0 auto;
  }

  .container > a {
    display: block;
    width: 160px;
    height: 40px;
    margin-top: 5px;
    padding-top: 3px;
    float: left;
  }
  .container > a img {
    width: 120px;
    float: left;
  }

  .container form {
    float: left;
    margin-top: 13px;
    margin-left: -20px;
  }
  .container form input {
    width: 233px;
    height: 26px;
    background: url("../assets/search.e53b380a.hashed.png") no-repeat 4px 4px #888;
    border-radius: 15px;
    padding: 3px 5px 3px 22px;
  }

  .container ul {
    float: right;
    margin-top: 5px;
  }
  .container ul li {
    float: left;
  }
  .container ul li a {
    display: block;
    height: 40px;
    line-height: 40px;
    font-size: 13px;
    padding: 0 15px;
  }
  .container ul li a:hover {
    color: #fff;
  }

</style>
