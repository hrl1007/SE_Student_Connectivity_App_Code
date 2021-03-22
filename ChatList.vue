<template>

    <div>

 <van-nav-bar title="Orz" nav-bar-text-color="white" style="background-color: rgb(1, 15, 31);color:white" left-text="Anthony Co rtez"  color="white" left-arrow>
  <van-icon name="tv-o"  size="25" slot="right"/>
  <van-icon name="phone-o" size="25"   slot="right" />
  
</van-nav-bar>       
        <section class="chatlist" :class="showSelBox>0?'chatlist-bottom-collapse':'chatlist-bottom'">
            <mt-loadmore :top-method="loadTop" top-pull-text="load more" top-drop-text="release" @top-status-change="handleTopChange" ref="loadmore">
                
                <ul>
                    <template v-for="item in records">
                        <li class="chat-mine" v-if="item.type==1">
                            <div class="chat-user"><img src="../assets/user.png"></div>
                            <div class="time"><cite><i>{{item.time}}</i>{{item.name}}</cite></div>
                            <div class="chat-text" v-html="replaceFace(item.content)"></div>
                        </li>
                        <li v-if="item.type==2">
                            <div class="chat-user"><img src="../assets/default.png"></div>
                            <div class="time"><cite>{{item.name}}<i>{{item.time}}</i></cite></div>
                            <div class="chat-text" v-html="replaceFace(item.content)"></div>
                        </li>
                    </template>
                    <li >
                            <div class="chat-user"><img src="../assets/default.png"></div>
                            <div class="time"><cite> Myname<i> </i></cite></div>
                            <div class="chat-text" >  <van-icon name="flag-o" /> A_Project_guide </div>
                        </li>
                </ul>
            </mt-loadmore>
        </section>


        <section class="foot">
            <!-- <mt-field id="txtContent" placeholder="Please input " class="con" v-model="content"></mt-field> -->
            
          <van-search
          style="background-color: rgb(1, 15, 31);color:white"
          left-icon="smile-o"
          size="30"
  v-model="value"
  show-action
  placeholder="Please inpiut Data"
  @search="onSearch"
>
  <div slot="action" @click="onSearch"> <van-icon name="volume-o" style="color:white"  size="25" slot="right"/></div>
</van-search>
            <span class="btn-face" v-on:click="showSelBox=showSelBox==1?0:1"><i class="fa fa-smile-o" aria-hidden="true"></i></span>
            <span class="btn-plus" v-on:click="showSelBox=showSelBox==2?0:2">  <van-icon name="tv-o"  size="30" slot="center"/></span>
            <!-- <span class="btn btn-send" v-on:click="sendMsg"><image src ="../assets/9.jpg"/></span> -->
            <section class="selbox" :class="showSelBox>0?'show':'hide'">
                <section v-show="showSelBox==1" class="face-box">
                    <mt-swipe :auto="0" :continuous="false">
                        <mt-swipe-item v-for="n in Math.ceil(EXPS.length/18)">
                            <li v-for="(item, index) in getEXP(n,18)">
                                <img :src="'static/emotion/'+item.file" alt="" :data="item.code" v-on:click="content+=item.code">
                            </li>
                        </mt-swipe-item>
                    </mt-swipe>
                </section>
                <div v-show="showSelBox==2">{{selOther}}</div>
              
            </section>
        </section>

    </div>
</template>

<script>
import util from '../common/util'
import { Toast } from 'mint-ui';

import { Loading } from 'vant'
export default {
    name: 'chatlist',
    data() {
        return {
            showSelBox: 0, 
            selFace: 'face motion',
            selOther: 'other function',
            content:'',
            topStatus: '',
           


            records: [ {
                type: 2,
                time: util.formatDate.format(new Date(),'yyyy-MM-dd hh:mm:ss'),
                name: 'A',
                content: 'Okay,I agree with all these points, Waiting for the results next Thursday.Have a good weekend!'
            },{
                type: 1,
                time: util.formatDate.format(new Date(),'yyyy-MM-dd hh:mm:ss'),
                name: 'B',
                content: 'Hi！Lina!I supposed not on this comp unfortunately!'
            },{
                type: 2,
                time: util.formatDate.format(new Date(),'yyyy-MM-dd hh:mm:ss'),
                name: 'B',
                content: 'Could you please send the guide to another format.for example,pdf?'
            },{
                type: 1,
                time: util.formatDate.format(new Date(),'yyyy-MM-dd hh:mm:ss'),
                name: 'A',
                content: 'A_Project_guide.pdf</a>'
            }],
            // 表情
            EXPS: [
                { file: '100.gif', code: '/::)', title: 'smile',reg:/\/::\)/g },
                { file: '101.gif', code: '/::~', title: '',reg:/\/::~/g },
                { file: '102.gif', code: '/::B', title: '',reg:/\/::B/g },
                { file: '103.gif', code: '/::|', title: '',reg:/\/::\|/g },
                { file: '104.gif', code: '/:8-)', title: '',reg:/\/:8-\)/g },
                { file: '105.gif', code: '/::<', title: '',reg:/\/::</g },
                { file: '106.gif', code: '/::$', title: '',reg:/\/::\$/g },
                { file: '107.gif', code: '/::X', title: '',reg:/\/::X/g },
                { file: '108.gif', code: '/::Z', title: '',reg:/\/::Z/g },
                { file: '109.gif', code: '/::\'(', title: '',reg:/\/::'\(/g },
                { file: '110.gif', code: '/::-|', title: '',reg:/\/::-\|/g },
                { file: '111.gif', code: '/::@', title: '',reg:/\/::@/g },
                { file: '112.gif', code: '/::P', title: '',reg:/\/::P/g },
                { file: '113.gif', code: '/::D', title: '',reg:/\/::D/g },
                { file: '114.gif', code: '/::O', title: '',reg:/\/::O/g },
                { file: '115.gif', code: '/::(', title: '',reg:/\/::\(/g },
                { file: '116.gif', code: '/::+', title: '',reg:/\/::\+/g },
                { file: '117.gif', code: '/:--b', title: '',reg:/\/:--b/g },
                { file: '118.gif', code: '/::Q', title: '',reg:/\/::Q/g },
                { file: '119.gif', code: '/::T', title: '',reg:/\/::T/g },
                { file: '120.gif', code: '/:,@P', title: '',reg:/\/:,@P/g },
                { file: '121.gif', code: '/:,@-D', title: '',reg:/\/:,@-D/g },
                { file: '122.gif', code: '/::d', title: '',reg:/\/::d/g },
                { file: '123.gif', code: '/:,@o', title: '' ,reg:/\/:,@o/g},
                { file: '124.gif', code: '/::g', title: '',reg:/\/::g/g },
                { file: '125.gif', code: '/:|-)', title: '' ,reg:/\/:\|-\)/g},
                { file: '126.gif', code: '/::!', title: '',reg:/\/::!/g },
                
            ]
        }
    },
    methods: {
        onSearch:function(){
            Toast("Daa");
        },
        getEXP: function (pageNow,pageSize) {
            return this.EXPS.slice((pageNow - 1) * pageSize, pageSize * pageNow)
        },

        sendMsg: function(){
            var _this=this;

            if(this.content==''){
                Toast('Please input ');
                return;
            }

            this.records.push({
                type: 1,
                time: util.formatDate.format(new Date(),'yyyy-MM-dd hh:mm:ss'),
                name: 'B',
                content: this.content
            });

            setTimeout(function(){
                _this.records.push({
                    type: 2,
                    time: util.formatDate.format(new Date(),'yyyy-MM-dd hh:mm:ss'),
                    name: 'A',
                    content: 'tests'
                });
            },100);

            this.content='';

            this.scrollToBottom();

        
        },
      
        focusTxtContent:function(){
            document.querySelector("#txtContent input").focus();
        },
     
        scrollToBottom:function(){
            setTimeout(function(){
                var chatlist = document.getElementsByClassName('chatlist')[0];
                chatlist.scrollTop=chatlist.scrollHeight;
            },100);
        },
      
        replaceFace:function(con){
            var _this=this;
            var exps=this.EXPS;
            for(var i=0;i<exps.length;i++){
                
                con = con.replace(exps[i].reg, '<img src="static/emotion/' + exps[i].file +'"  alt="" />');
            }
            return con;
        },
        handleTopChange(status) {
            this.topStatus = status;
        },
        loadTop(id) {
            var _this=this;
            setTimeout(() => {
                var chatlist = document.getElementsByClassName('chatlist')[0];
                var oldHeight=chatlist.scrollHeight;

                _this.records.unshift({
                    type: 1,
                    time: util.formatDate.format(new Date(),'yyyy-MM-dd hh:mm:ss'),
                    name: 'B',
                    content: 'HI'
                }, {
                    type: 2,
                    time: util.formatDate.format(new Date(),'yyyy-MM-dd hh:mm:ss'),
                    name: 'Hello',
                    content: 'hi,i am ok!'
                });

                setTimeout(function(){
                    var newHeight=chatlist.scrollHeight;
                    chatlist.scrollTop=newHeight-oldHeight;
                },100);

                this.$refs.loadmore.onTopLoaded(id);
            }, 1500);
        }
    },
    mounted:function(){
        this.scrollToBottom();
        this.focusTxtContent();
    }
    // updated:function(){
    //     this.scrollToBottom();
    // }
}
</script>

<style>
.name {
    color: white;
}
    .chatlist {
        position: absolute;
        top: 60px;
        bottom: 48px;
        left: 0px;
        right: 0px;
        overflow-y: scroll;
        overflow-x: hidden;
        padding: 10px;
    }
    
    .chatlist-bottom {
        bottom: 48px;
    }
    
    .chatlist-bottom-collapse {
        bottom: 198px;
    }
    
    .chatlist ul {
        min-height: 300px;
    }
    
    .chatlist ul .chat-mine {
        text-align: right;
        padding-left: 0;
        padding-right: 60px;
    }
    
    .chatlist ul li {
        position: relative;
        /*font-size: 0;*/
        margin-bottom: 10px;
        padding-left: 60px;
        min-height: 68px;
    }
    
    .chat-mine .chat-user {
        left: auto;
        right: 3px;
    }
    
    .chat-user {
        position: absolute;
        left: 3px;
    }
    
    .chat-text,
    .chat-user {
        display: inline-block;
        vertical-align: top;
        /*font-size: 14px;*/
    }
    
    .chat-user img {
        width: 40px;
        height: 40px;
        border-radius: 100%;
    }
    
    .time {
        width: 100%;
    }
    
    cite {
        left: auto;
        right: 60px;
        text-align: right;
    }
    
    cite {
        font-style: normal;
        line-height: 24px;
        font-size: 12px;
        white-space: nowrap;
        color: #999;
        text-align: left;
    }
    
    cite i {
        font-style: normal;
        padding-left: 5px;
        padding-right: 5px;
        font-size: 12px;
    }
    
    .chat-mine .chat-text {
        margin-left: 0;
        text-align: left;
        background: -webkit-linear-gradient(left,hsla(0,0%,59%,.35),rgb(255, 102, 0),rgb(247, 119, 1)) no-repeat;
        color: #fff;
    }
    
    .chat-text {
        position: relative;
        line-height: 22px;
        /*margin-top: 25px;*/
        padding: 10px 15px;
        background: -webkit-linear-gradient(left,rgb(255, 94, 0),rgb(247, 161, 1)) no-repeat;
        border-radius: 3px;
        color: #333;
        word-break: break-all;
        max-width: 462px\9;
    }
    
    .chat-text,
    .chat-user {
        display: inline-block;
        vertical-align: top;
        font-size: 14px;
    }
    
    .chat-text img {
        max-width: 100%;
        vertical-align: middle;
    }
    
    .chat-user {
        position: absolute;
        left: 3px;
    }
    
    .chat-text:after {
        content: '';
        position: absolute;
        left: -10px;
        top: 15px;
        width: 0;
        height: 0;
        border-style: solid dashed dashed;
        border-color: #eee transparent transparent;
        overflow: hidden;
        border-width: 10px;
    }
    
    .chat-mine .chat-text:after {
        left: auto;
        right: -10px;
        border-top-color: #33DF83;
    }
    
    .foot {
        width: 100%;
        min-height: 48px;
        position: fixed;
        bottom: 0px;
        left: 0px;
         background-color: rgb(1, 15, 31);
    }
    
    .foot .con {
        position: absolute;
        left: 66px;
        right: 40px;
    }
    
    .foot .btn-plus {
        width: 28px;
        padding: 9px 3px;
        position: absolute;
        left: 0px;
        border-left: 1px solid #d9d9d9;
    }
    
    .foot .btn-plus i {
        font-size: 2em;
        color: #ccc;
    }
    
    .foot .btn-face {
        width: 28px;
        padding: 9px 3px 9px 0px;
        position: absolute;
        left: 35px;
        /*border-right: 1px solid #d9d9d9;*/
    }
    
    .foot .btn-face i {
        font-size: 2em;
        color: #d9d9d9;
    }
    
    .foot .selbox {
        height: 150px;
        margin-top: 48px;
        border-top: 1px solid #d9d9d9;
    }
    
    .show {
        display: block;
    }
    
    .hide {
        display: none;
    }
    
    .face-box {
        /* position: absolute; */
        /* top: 48px; */
        /* left: 0px; */
        /* right: 0px; */
        /* bottom: 0px; */
        padding: 15px 15px 0px 15px;
        overflow: hidden;
        width: 290px;
        margin: 0px auto;
        height: 135px;
    }
    
    .face-box li {
        width: 30px;
        float: left;
        padding: 6px 10px 0px 8px;
    }
    
    .btn {
        display: inline-block;
        vertical-align: top;
        font-size: 14px;
        line-height: 32px;
        margin-left: 5px;
        padding: 0 6px;
        background-color: #33DF83;
        color: #fff;
        border-radius: 3px;
    }
    
    .btn-send {
        position: absolute;
        right: 0px;
        top: 8px;
    }
</style>

