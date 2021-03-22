<template>
  <div id="search">
    <div style="margin:5% 0 0 3%; font-size:28px; font-weight:700">
      Search
    </div>

<div style="margin:1% 3%; ">
    <el-autocomplete class="inline-input" v-model="state1" :fetch-suggestions="querySearch" prefix-icon="el-icon-search" placeholder="Search" @select="handleSelect"></el-autocomplete>
    <div class="text" style="margin-left:-3%">Recent Search</div>
    <div v-for="recent in recents" :key="recent"><van-icon name="search" style="font-weight:900; margin-right:2%"/>{{recent.value}}</div>
</div>


<div style="padding:3%;">
    <div style="float:left"><el-avatar :size="50" :src="UserUrl"></el-avatar></div>
    <div class="Username" style="float:left;margin:3% 0 0 5%">
        Ricky Willis
    </div>
</div>

<div class="text">Recommend</div>

    <div class="block" v-for="Moments in friendsmesg" :key="Moments">

      <div style="clear:both;">
        <div style="float:left; width:15%;"><el-avatar :size="50" :src="Moments.UserUrl"></el-avatar></div>
        <div style="float:left; width:75%; margin-left:3%; ">
          <div class="Username">{{Moments.Username}}</div>
          <div>
            <span class="time">{{Moments.time}}</span>&nbsp;&nbsp;<van-icon name="location" />&nbsp;<span style="font-size:14px">{{Moments.location}}</span>
          </div>
        </div>
        <div style="font-size:24px; font-weight:700"><van-icon name="ellipsis" /></div>   
      </div>

        <van-row style="clear:both; margin-top:10%">
            <van-col span="16">
                <div>{{Moments.mesg}}</div>
                <div>Model：{{Moments.mesg1}}</div>
                <div>Make up：{{Moments.mesg2}}</div>
            </van-col>
            
            <van-col span="8">
                <van-image width="125" height="125" :src="Moments.ModelUrl"/>
            </van-col>
        </van-row>

      <div style="margin-top:3%;">
        <van-icon v-show="!pinkLike" @click="pinkLike = !pinkLike" class="icon" name="like-o" />
        <van-icon v-show="pinkLike" @click="pinkLike = !pinkLike" color="#f5224a" class="icon" name="like" /><span style="margin:2.5%;">{{Moments.olikes}}</span>
        <i class="el-icon-chat-round"/><span style="margin:3%; ">{{Moments.omesg}}</span>
        <van-icon class="icon" name="share-o" @click="showShare = true"/>
        <van-share-sheet v-model="showShare" title="Share to friends" :options="options"/>
        <van-icon v-show="!orange" @click="orange = !orange" class="icon" name="star-o" style="float:right"/>
        <van-icon v-show="orange" @click="orange = !orange" color="#ff4d07" class="icon" name="star" style="float:right"/>

      </div>

    </div>
 <br><br><br><br>
<!-- <van-tabbar v-model="active" class="tabbar" active-color="#fff">
  <van-tabbar-item icon="wap-home"></van-tabbar-item>
  <van-tabbar-item icon="search"></van-tabbar-item>
  <van-tabbar-item icon="chat" badge="5"></van-tabbar-item>
  <van-tabbar-item icon="bell"></van-tabbar-item>
  <van-tabbar-item icon="manager"></van-tabbar-item>
</van-tabbar> -->

  </div>
</template>

<script>
import { Toast } from 'vant';
export default {
  data () {
    return {
      recentSearch: [],
      recents: [
        {value: 'UI/UX'},
        {value: 'Design'},
      ],
      state1: '',
      active: 1,
      UserUrl:'https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png',
      pinkLike:false,
      orange:false,
      showShare: false,
      options: [
        [
          { name: 'Wechat', icon: 'wechat' },
          { name: 'Weibo', icon: 'weibo' },
          { name: 'QQ', icon: 'qq' },
          { name: 'Link', icon: 'link' },
          { name: 'Poster', icon: 'poster' },
        ],
        [
          { name: 'QR code', icon: 'qrcode' },
          { name: 'weapp-qrcode', icon: 'weapp-qrcode' },
        ],
      ],
      friendsmesg:[
      {
        Username:'Allie Hall',
        UserUrl:'https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png',
        time:'18 hours ago',
        location:'Newark, United States',
        mesg:'A shot from recent beauty photoshoot.',
        mesg1:'Elizabeth Rivera',
        mesg2:'Amy Christensen',
        ModelUrl:'https://img01.yzcdn.cn/vant/cat.jpeg',
        olikes:'534',
        omesg:'25',
      },
      {
        Username:'Lelia hayes',
        UserUrl:'https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png',
        time:'Yesterday',
        location:'Jenny Lake, United States',
        mesg:'A shot from recent beauty photoshoot.',
        mesg1:'Elizabeth Rivera',
        mesg2:'Amy Christensen',
        ModelUrl:'https://img01.yzcdn.cn/vant/cat.jpeg',
        olikes:'534',
        omesg:'25',
      },
      ],
      

    }
  },

    methods: {
      querySearch(queryString, cb) {
        var recentSearch = this.recentSearch;
        var results = queryString ? recentSearch.filter(this.createFilter(queryString)) : recentSearch;
        cb(results);
      },
      createFilter(queryString) {
        return (recentSearc) => {
          return (recentSearc.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0);
        };
      },
      loadAll() {
        return [
          { "value": "UI/UX" },
          { "value": "Design"},
        ];
      },
      handleSelect(item) {
        console.log(item);
      }
    },
    mounted() {
      this.recentSearch = this.loadAll();
    }



}
</script>

<style>
#search{
  background-color:#10101a;
  color: white;
  line-height: 28px;
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
}
.inline-input{
    width: 100%;   
}
.text{
    margin-top:3%; 
    clear:both; 
    padding:3%;  
    color:#757380;
}
.block{
    margin-top:3%;
    background-color:#1c1c26; 
    border:1px solid white; 
    border-radius: 20px;
    padding:3%;
}
.Username{
  font-weight: 600;
}
.time{
  font-size: 14px;
  color: #b5b3b9;
}
.icon,.el-icon-chat-round{
  font-size: 28px;
}
/* .tabbar{
  background-color: #1a1c28;
  border:3px solid #5874a4; 
  border-radius: 15px 15px 0 0;  
} */

</style>
