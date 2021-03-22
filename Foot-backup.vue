<template>
  <section class="foot">
    <mt-field placeholder="Input" class="con"></mt-field>
    <!-- <input type="text" placeholder="Please input  your data  "></input  > -->
    <span class="btn-face" v-on:click="showSelBox=showSelBox==1?0:1"><i class="fa fa-smile-o" aria-hidden="true"></i></span>
    <span class="btn-plus" v-on:click="showSelBox=showSelBox==2?0:2"><i class="fa" aria-hidden="true" :class="showSelBox==2?'fa-minus-circle':'fa-plus-circle'"></i></span>
    <section class="selbox" :class="showSelBox>0?'show':'hide'">
      <section v-if="showSelBox==1" class="face-box">
        <mt-swipe :auto="0">
          <mt-swipe-item v-for="n in Math.ceil(EXPS.length/18)">
            <li v-for="(item, index) in getEXP(n)">
              <img :src="'static/emotion/'+item.file" alt="" :data="item.code">
            </li>
          </mt-swipe-item>
        </mt-swipe>
      </section>
      <div v-if="showSelBox==2">{{selOther}}</div>
      <div v-else></div>
    </section>
  </section>
</template>

<script>
export default {
  name: 'foot',
  data () {
    return {
      showSelBox: 0, 
      selFace: 'motion',
      selOther: 'OtherFunction',
      EXPS: [
        { file: '171.gif', code: '/:kn', title: '' },
        { file: '172.gif', code: '/:footb', title: '' },
        { file: '173.gif', code: '/:ladybug', title: '' },
        { file: '174.gif', code: '/:shit', title: '' },
        { file: '175.gif', code: '/:moon', title: '' },
        { file: '176.gif', code: '/:sun', title: '' },
        { file: '177.gif', code: '/:gift', title: '' },
        { file: '178.gif', code: '/:hug', title: '' },
        { file: '179.gif', code: '/:strong', title: '' },
        { file: '180.gif', code: '/:weak', title: '' },
        { file: '181.gif', code: '/:share', title: '' },
        { file: '182.gif', code: '/:v', title: '' },
        { file: '183.gif', code: '/:@)', title: '' },
        { file: '184.gif', code: '/:jj', title: '' },
        { file: '185.gif', code: '/:@@', title: '' },
        { file: '186.gif', code: '/:bad', title: '' },
        { file: '187.gif', code: '/:lvu', title: '' },
        { file: '188.gif', code: '/:no', title: '' },
        { file: '189.gif', code: '/:ok', title: 'ok' },
        { file: '190.gif', code: '/:love', title: '' },
        { file: '191.gif', code: '/:<L>', title: '' },
        { file: '192.gif', code: '/:jump', title: '' },
        { file: '193.gif', code: '/:shake', title: '' },
        { file: '194.gif', code: '/:<O>', title: '' },
        { file: '195.gif', code: '/:circle', title: '' },
        { file: '196.gif', code: '/:kotow', title: '' },
        { file: '197.gif', code: '/:turn', title: '' },
        { file: '198.gif', code: '/:skip', title: '' },
        { file: '199.gif', code: '/:oY', title: '' }
      ]
    }
  },
  methods: {
    getEXP: function (pageNow) {
      return this.EXPS.slice((pageNow - 1) * 18, 18 * pageNow)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .foot {
    width: 100%;
    min-height: 48px;
    position: fixed;
    bottom: 0px;
    left: 0px;
     background-color: rgb(1, 15, 31);s
  }
  
  .foot .con {
    position: absolute;
    left: 40px;
    right: 40px;
  }
  
  .foot .btn-plus {
    width: 30px;
    height: 30px;
    padding: 9px 5px;
    position: absolute;
    right: 0px;
    border-left: 1px solid rgb(25, 62, 105);
  }
  
  .foot .btn-plus i {
    font-size: 2.2em;
    color: #ccc;
  }
  
  .foot .btn-face {
    width: 30px;
    height: 30px;
    padding: 9px 5px;
    position: absolute;
    left: 0px;
    border-right: 1px solid #d9d9d9;
  }
  
  .foot .btn-face i {
    font-size: 2.2em;
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
</style>