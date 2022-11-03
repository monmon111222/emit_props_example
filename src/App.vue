<template>
  <div id="app">
    <div class="about">
      <SearchForm
        :searchText="searchTextFromParent"
        @search="(key) => searKey(key)"
      />
      <!-- @search="searKey"  -->
    </div>
  </div>
</template>
<script>
import SearchForm from '@/components/SearchForm'

export default {
  name: 'App',
  components: { SearchForm },
  data() {
    return {
      searchTextFromParent: ''
    }
  },
  created() {},
  methods: {
    searKey(val) {
      console.log('賦值前 ', this.searchTextFromParent, '子元件修改後的值', val)
      this.searchTextFromParent = val
      console.log('賦值後', this.searchTextFromParent, '子元件修改後的值', val)
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
