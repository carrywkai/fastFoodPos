<template>
  <div id="app">
    <!-- 左边导航栏组件 -->
    <left-nav></left-nav>
    <router-view/>
  </div>
</template>

<script>
import leftNav from '@/components/leftNav'
export default {
  name: 'App',
  components: {
    leftNav
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
