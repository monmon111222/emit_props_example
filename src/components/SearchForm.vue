<template>
  <div class="search-form">
    <el-input
      class="search-input"
      v-model="inputText"
      placeholder="搜尋..."
    ></el-input>
    <el-button icon="el-icon-search" circle @click="search()"></el-button>
  </div>
</template>

<script>
export default {
  name: 'SearchForm',
  // 父元件傳遞進來的參數
  props: {
    searchText: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      inputText: ''
    }
  },
  created() {
    this.inputText = this.searchText
  },
  methods: {
    search() {
      // 傳遞/回傳給付元件的事件
      this.$emit('search', this.inputText)
    }
  }
}
</script>

<style scoped lang="scss">
.search-form {
  display: flex;
  justify-content: center;
  .search-input {
    width: 150px;
  }
}
</style>
