<template>
  <div>
    <router-view />
    <van-tabbar v-model="active" class="tabbar" active-color="#fff">
    <van-tabbar-item replace to="/home" icon="wap-home"></van-tabbar-item>
    <van-tabbar-item replace to="/search" icon="search"></van-tabbar-item>
    <van-tabbar-item replace to="/mesg" icon="chat" badge="5"></van-tabbar-item>
    <van-tabbar-item replace to="/mesg1" icon="bell"></van-tabbar-item>
    <van-tabbar-item replace to="/personal" icon="manager"></van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<script>
export default {
  data () {
    return {
      active: 1
    }
  }
}
</script>

<style>
.tabbar{
  background-color: #1a1c28;
  border:3px solid #5874a4; 
  border-radius: 15px 15px 0 0;  
}
</style>
