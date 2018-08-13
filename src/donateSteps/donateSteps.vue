<template>
  <div class="index">
    <div class="step-container">
      <div class="step-title">
        兑健康每日捐步打卡
      </div>
      <div class="step-content">
        <div class="step-detail">
          <x-circle
            :percent="percent"
            :stroke-width="7"
            :trail-width="3"
            stroke-color="#FFD100"
            trail-color="#FFF6E9">
            <span v-if="isDonated">
              <p class="notice">捐步成功</p>
              <p class="notice">感谢您的爱心</p>
            </span>
            <span v-else>
              <p class="today-steps">今日步数</p>
              <p>{{ totalSteps }}</p>
            </span>
          </x-circle>
        </div>
        <div v-if="isDonated">

        </div>
        <div v-else>
          <div v-if="stepNote === '0'">
            <p class="need-steps">还差{{ needSteps }}步，即可捐步</p>
          </div>
          <div v-else-if="stepNote === '1'">
            <p class="need-steps">距离5000步还差{{ needSteps }}步</p>
          </div>
          <div v-else-if="stepNote === '2'">
            <p class="need-steps">距离10000步还差{{ needSteps }}步</p>
          </div>
          <div v-else-if="stepNote === '3'">
            <p class="need-steps">距离50000步还差{{ needSteps }}步</p>
          </div>
          <div v-else>
            <p class="need-steps">非常棒，一天的运动量已到达</p>
          </div>
      </div>
        <x-button v-if="clickAble" class="donate-btn" @click.native.prevent="donateSteps"> 立即捐步 </x-button>
        <x-button v-else class="donate-btn-disable"> 立即捐步 </x-button>
      </div>
      <ul class="donate-info">
        <li>
            <p class="donate-data">1000步</p>
            <p class="donate-text">我已捐赠</p>
        </li>
        <li>
            <p class="donate-data">10元</p>
            <p class="donate-text">累计金额</p>
        </li>
        <li>
          <p class="donate-data">第999名</p>
          <p class="donate-text">社区排名</p>
        </li>
      </ul>

    </div>
    <div class="donate-object">
      <div class="donate-title">
        援助山区贫困儿童
      </div>
      <p class="need-steps">距离目标还有{{ needSteps }}元</p>
      <x-progress :percent="goalPercent" :show-cancel="false" class="donate-progress"></x-progress>
      <p class="goal-steps">捐赠目标:50000元</p>
    </div>

    <div class="explain">
      <div class="explain-title">
        捐步活动介绍
      </div>
      <p class="donate-explain">
        进馆参观游客，在游玩结束后查看自己的运动步数，超过10000步，截图至杭州长乔极地海洋公园官方微信，即可帮助“星星儿童”获得杭州长乔极地海洋公园出资的1元捐款。 
      </p>
    </div>
  </div>
</template>

<style scoped lang="less">
.index{
  width: 100%;
  margin: 0;
  padding: 0;
  position: absolute;
  top: 0;
  // bottom: 0;
  left: 0;
  right: 0;
  text-align: center;
  overflow: hidden;
  .step-container{
    margin: 45px 30px 0 30px;
    // height: 400px;
    // border: 1px solid blue;
    // margin-bottom: 200px;
    .step-title{
      color: #333333;
      text-align: left;
      font-size: 20px;
      line-height: 28px;
      padding: 10px 0;
    }
    .step-content{
      // height: 253px;
      text-align: center;
      // border: 1px solid red;
      // margin: 20px 0;
      .step-detail{
        margin: 30px auto;
        width:120px;
        height: 120px;
        // border: 2px solid black;
        // border-radius: 50%;
        p{
          position: relative;
          color: #333333;
          font-size: 20px;
          // top: 50%;
          // transform: translateY(-50%);
        }
        .notice{
          color: #333333;
          font-size: 14px;
        }
        .today-steps{
          color: #999999;
          font-size: 10px;
        }
      }
      .need-steps{
        // margin: 10px;
        color: #666666;
        font-size: 12px;
      }
      .donate-btn{
        color: #FFFFFF;
        line-height: 40px;
        margin-top: 14px;
        margin-bottom: 20px;
        font-size: 14px;
        background: rgba(255,209,0,1);
        box-shadow: 0px 2px 2px 0px rgba(255,236,148,1);
        border-radius: 20px;
      }
      .donate-btn-disable{
        color: #979797;
        line-height: 40px;
        margin-top: 14px;
        margin-bottom: 20px;
        font-size: 14px;
        background:rgba(237,237,237,1);
        border-radius: 20px;
      }
    }
    .donate-info{
      height: 80px;
      text-align: center;
      list-style: none;
      border: 1px solid red;
      display: flex;
      justify-content: space-between;
      // justify-content: center;
      li{
        display: inline-block;
        flex: 1;
        justify-content: convert;
        overflow: hidden;
        // height: 60px;
        border: 1px solid black;
        padding: 8px;
        li:nth-child(1){
          justify-content: flex-start;
          // text-align: left;
        }
        li:nth-child(3){
          justify-content: flex-end;
        }
        .donate-data{
          font-size: 18px;
          color: #333333;
        }
        .donate-text{
          font-size: 12px;
          color: #666666;
        }
      }
    }
  }
  .donate-object{
    margin: 0px 30px;
    // height: 100px;
    // border: 1px solid red;
    overflow: hidden;
    .donate-title{
      // background: green;
      color: #333333;
      text-align: left;
      font-size: 20px;
      line-height: 28px;
      padding: 10px 0;
    }
    .need-steps{
      font-size: 10px;
      color: #FFD100;
    }
    .donate-progress{
      margin: 10px 0 ;
      // border: 2px solid rgba(255,209,0,1);
    }
    .goal-steps{
      color: #666666;
      font-size: 10px;
      // float: right;
      text-align: right;
    }
  }
  .explain{
    margin: 0px 30px;
    // border: 1px solid black;
    // height: 100px;
    text-align: left;
    .explain-title{
      color: #333333;
      font-size: 20px;
      line-height: 28px;
      padding-top: 20px;
      padding-bottom: 10px;
    }
    .donate-explain{
      color: #333333;
      font-size: 12px;
    }
  }
}
</style>

<script>
import { XCircle, XButton, XProgress } from 'vux'
export default {
  components: {
    XCircle,
    XButton,
    XProgress
  },
  data () {
    return {
      totalSteps: 2000,
      // needSteps: 20,
      stepNote: '0',
      isDonated: false
    }
  },
  computed: {
    percent () {
      if (this.isDonated) {
        return 0
      } else {
        return this.totalSteps / 50000 * 100
      }
    },
    goalPercent () {
      return this.totalSteps / 200000 * 100
    },
    needSteps () {
      if (this.totalSteps < 100) {
        this.stepNote = '0'
        return 100 - this.totalSteps
      } else if (this.totalSteps > 100 && this.totalSteps < 5000) {
        this.stepNote = '1'
        return 5000 - this.totalSteps
      } else if (this.totalSteps > 5000 && this.totalSteps < 10000) {
        this.stepNote = '2'
        return 10000 - this.totalSteps
      } else if (this.totalSteps > 10000 && this.totalSteps < 50000) {
        this.stepNote = '3'
        return 50000 - this.totalSteps
      } else {
        return 0
      }
    },
    clickAble () {
      if (this.totalSteps > 100 && !this.isDonated) {
        return true
      } else {
        return false
      }
    }
  },
  methods: {
    donateSteps () {
      this.isDonated = true
      // demo of ajax
      const Axios = require('axios')
      Axios.get('http://localhost:8080/package.json')
      .then(function (response) {
        debugger
        console.log(response)
      })
      .catch(function (error) {
        console.log(error)
      })
    }
  }
}
</script>

