<template>
  <div id='app'>
    <leftNav>
    </leftNav>
    <div class='main'>
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import leftNav from '@/components/common/leftnav'
export default {
  name: 'app',
  components:{
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
  height: 100%;
}
.main {
  float: left;;
  width: 95%;
  background-color:floralwhite;
  height: 100%;
  padding-bottom: 0%;
}
</style>
