<template>
  <div class="donate-steps">
    <div class="donate-header">
      <img class="back-btn" src="../../assets/arrow.png" alt="">
      <p class="title">捐步</p>
    </div>
    <div class="donate-container">
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
                <p>{{ todaySteps }}</p>
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
              <p class="donate-data">{{ donateData.donatedSteps }}步</p>
              <p class="donate-text">我已捐赠</p>
          </li>
          <li>
              <p class="donate-data">{{ donateData.donatedMoney }}元</p>
              <p class="donate-text">累计金额</p>
          </li>
          <li>
            <p class="donate-data">第{{ donateData.rank }}名</p>
            <p class="donate-text">社区排名</p>
          </li>
        </ul>

      </div>
      <div class="donate-object">
        <div class="donate-title">
          援助山区贫困儿童
        </div>
        <p class="need-steps">距离目标还有{{ donateData.leftMoney }}元</p>
        <x-progress :percent="goalPercent" :show-cancel="false" class="donate-progress"></x-progress>
        <p class="goal-steps">捐赠目标:{{ donateData.targetDonateMoney }}元</p>
      </div>

      <div class="explain">
        <div class="explain-title">
          活动细则
        </div>
        <ul class="donate-explain">
          <li>1.每人每日捐赠上限50000步</li>
          <li>2.每10000步等于1元,100步起捐</li>
          <li>3.每日只能捐赠一次,第二天0点将清空前一天步数</li>
          <li>4.参与方式:“奥悦家”APP主页右下角活动宣传栏</li>
          <li>5.活动时间:2018年09月15日-2018年09月20日</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped lang="less">
.donate-steps{
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
  background-image: url('../../assets/bg-donate-steps.jpg');
  background-color: #FFD100;
  .donate-header{
    z-index: 1000px;
    // background: #FFD100;
    position: relative;
    height: 40px;
    // border: 1px solid red;
    text-align: center;
    font-size: 24px;
    color: #333333;
    .back-btn{
      position: absolute;
      width: 20px;
      height: 20px;
      margin: 10px;
      left: 13px;
    }
    .title{
      // position: absolute;
      line-height: 40px;
    }
  }
  .donate-container{
    background: #FFFFFF;
    margin: 0px 17px 10px 17px;
    border-radius: 13px;
    .step-container{
      margin: auto 13px;
      padding-top: 20px;
      // border: 1px solid blue;
      .step-title{
        color: #333333;
        text-align: left;
        font-size: 20px;
        font-weight: Bold;
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
        // border: 1px solid red;
        display: flex;
        justify-content: space-between;
        // justify-content: center;
        li{
          display: inline-block;
          flex: 1;
          justify-content: convert;
          overflow: hidden;
          // height: 60px;
          // border: 1px solid black;
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
            padding-bottom: 10px;
          }
          .donate-text{
            font-size: 12px;
            color: #666666;
          }
        }
      }
    }
    .donate-object{
      margin: 10px 13px 0 13px;
      // height: 100px;
      // border: 1px solid red;
      overflow: hidden;
      .donate-title{
        // background: green;
        color: #333333;
        text-align: left;
        font-size: 20px;
        font-weight: Bold;
        line-height: 28px;
        padding: 10px 0;
      }
      .need-steps{
        padding-top: 10px;
        font-size: 10px;
        color: #FFD100;
      }
      .donate-progress{
        margin: 10px 0 ;
        // z-index: 100px;
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
      margin: 10px 13px 0 13px;
      // border: 1px solid black;
      // height: 100px;
      text-align: left;
      .explain-title{
        color: #333333;
        font-size: 20px;
        font-weight: Bold;
        line-height: 28px;
        padding-top: 20px;
        padding-bottom: 10px;
      }
      .donate-explain{
        list-style: none;
        color: #333333;
        font-size: 12px;
      }
    }
  }
}
</style>

<script>
import { XCircle, XButton, XProgress } from 'vux'
import Axios from 'axios'
import Util from 'utils/utils'
export default {
  components: {
    XCircle,
    XButton,
    XProgress
  },
  data () {
    return {
      todaySteps: 0,
      encyptSteps: 0,
      donateData: '',
      // donatedSteps: 0,
      // donatedMoney: 0,
      // rank: 1,
      // needSteps: 20,
      url: `http://activity.aylives.cn/donateSteps/h5/index?steps=${600}&encyptSteps=${88}`,
      stepNote: '0',
      isDonated: false
    }
  },
  created () {
    this.init()
  },
  computed: {
    percent () {
      if (this.isDonated) {
        return 0
      } else {
        if (this.todaySteps >= 50000) {
          return 100
        } else {
          return this.todaySteps / 50000 * 100
        }
      }
    },
    goalPercent () {
      let totalDonatedMoney = this.donateData.targetDonateMoney - this.donateData.leftMoney
      return totalDonatedMoney / this.donateData.targetDonateMoney * 100
    },
    needSteps () {
      if (this.todaySteps < 100) {
        this.stepNote = '0'
        return 100 - this.todaySteps
      } else if (this.todaySteps > 100 && this.todaySteps < 5000) {
        this.stepNote = '1'
        return 5000 - this.todaySteps
      } else if (this.todaySteps > 5000 && this.todaySteps < 10000) {
        this.stepNote = '2'
        return 10000 - this.todaySteps
      } else if (this.todaySteps > 10000 && this.todaySteps < 50000) {
        this.stepNote = '3'
        return 50000 - this.todaySteps
      } else {
        return 0
      }
    },
    clickAble () {
      if (this.todaySteps > 100 && !this.isDonated) {
        return true
      } else {
        return false
      }
    }
  },
  methods: {
    init () {
      // 获取app传过来的步数
      let data = this.getParam()
      if (data) {
        this.todaySteps = data[0].split('=', 2)[1]
        this.encyptSteps = data[1].split('=', 2)[1]
      }
      this.getDonateData()
    },
    getParam () {
      // http://donatesteps.frp.aylives.cn:8000/#/donateSteps?steps=2000&encyptSteps=88
      let href = window.location.href
      if (href.indexOf('?') > -1) {
        // 拆分url获取步数
        let data = href.split('?', 2)[1].split('&', 2)
        return data
      } else {
        return null
      }
    },
    getDonateData () {
      let token = Util.getCookie('token')
      let params = {
        params: {token: token}
      }
      Axios.get('src/donateSteps/data.json', params).then(res => {
        if (res.data && res.data.data) {
          this.donateData = res.data.data
        }
      })
    },
    donateSteps () {
      this.isDonated = true
      // 捐赠步数
      // let token = Util.getCookie('token')
      // let params = {
      //   token: token
      // }
      // Axios.post('..url', params).then(res => {
      // 刷新数据
      this.getDonateData()
      // })
    }
  }
}
</script>

