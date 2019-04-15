<template>
  <div>
    <div class="userInfo">
      <!-- loading -->
      <div class="loading" v-if="isLoading">
        <img src="../assets/loading.gif" title="加载中...">
      </div>

      <!-- 用户信息-->
      <div class="userInfomation">
        <div class="panel">
          <div class="header">
            <ul class="breadcrumb">
              <li></li>
            </ul>
          </div>
          <div class="inner"></div>
        </div>
        <div class="panel"></div>
        <div class="panel"></div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "UserInfo",
    data() {
      return {
        isLoading: false,
        userInfo: {}
      }
    }
  }
</script>

<style scoped>
  .userInfomation {
    padding: 0;
    margin-right: 305px;
    border: 1px solid red;
  }
  .panel {
    margin-bottom: 13px;
    border: 1px solid green;
  }
  .panel .header {
    padding: 10px;
    background-color: #f6f6f6;
    border-radius: 3px 3px 0 0;
  }
  .header .breadcrumb {
    padding: 0;
    margin: 0;
    border: none;
    background: 0 0;
    box-shadow: none;
    border-radius: 4px;
  }
  .panel .inner {
    padding: 10px;
    border-top: 1px solid #e5e5e5;
    border-radius: 0 0 3px 3px;
    background-color: #fff;
    line-height: 2em;

  }
</style>
