<template>
  <div class="pagination">
    <button @click="firstPage"><<</button>
    <button v-show="judegPageBtns">...</button>
    <button @click="changeBtn(btn)" v-for="btn in pageBtns" :class="{currentPage: currentPage === btn}">
      {{ btn }}
    </button>
    <button v-show="this.currentPage > this.pageBtns[this.pageBtns.length - 1] - 5">...</button>
    <button @click="lastPage">>></button>
  </div>
</template>

<script>
  export default {
    name: "Pagination",
    data() {
      return {
        pageBtns: [1, 2, 3, 4, 5],
        currentPage: 1
      }
    },

    methods: {
      changeBtn(page) {
        this.currentPage = page
        if (this.currentPage === this.pageBtns[this.pageBtns.length - 1]) {
          this.pageBtns.shift()
          this.pageBtns.push(this.pageBtns[this.pageBtns.length - 1] + 1)

        } else if (this.currentPage === this.pageBtns[0] && this.pageBtns[0] !== 1) {
          this.pageBtns.pop()
          this.pageBtns.unshift(this.pageBtns[0] - 1)
        }
        this.$emit('handle', this.currentPage)
      },
      firstPage() {
        this.currentPage = 1
        this.pageBtns = [1, 2, 3, 4, 5]
        this.$emit('handle', this.currentPage)
      },
      lastPage() {
        this.currentPage = this.pageBtns[this.pageBtns.length - 1]
        this.$emit('handle', this.currentPage)
      }
    },
    computed: {
      judegPageBtns() {
        var index = this.pageBtns.indexOf(1)
        return index === -1 ? true : false
      }
    }
  }
</script>

<style scoped>
  .pagination {
    border: 1px solid #ddd;
    border-radius: 4px;
    box-shadow: none;
    background-color: #fff;
    display: inline-block;
    height: 32px;
    line-height: 32px;
    margin: 10px 0 10px 10px;
  }
  button {
    width: 40px;
    vertical-align: top;
    background-color: transparent;
    cursor: pointer;
    border: none;
    outline: none;
    padding: 0 12px;
    height: 30px;
    line-height: 30px;
    font-size: 14px;
    text-decoration: none;
    border-right: 1px solid #ddd;
    float: left;
    text-align: center;
    white-space: nowrap;
  }
  button:hover {
    background: #f5f5f5;
  }
  button:last-child {
    border: none;
  }
  .currentPage {
    color: #80bd01;
    cursor: default;
  }
</style>
