<template>
  <div id="app">
    <InfiniteScroll />
  </div>
</template>

<script>
import InfiniteScroll from './components/InfiniteScroll.vue'

export default {
  name: 'app',
  components: {
    InfiniteScroll
  }
}
</script>

<style lang="scss">
  body {
    background-color: #04525A;
    margin: 0;
    padding: 0;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    color: #fff;
    font-size: 1.4rem;
    padding: 20px;
  }
</style>
