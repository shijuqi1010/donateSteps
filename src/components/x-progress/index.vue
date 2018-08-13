<template>
  <div class="weui-progress">
    <div class="weui-progress__bar">
      <div class="weui-progress__inner-bar" :style="{width: percent + '%'}">
      </div>
      <img src="../../assets/run.png" :style="{left: percent + '%'}">
      
    </div>
    <i v-if="percent === 100" class="weui-icon-success"></i>
    <i v-else class="weui-icon-success-circle"></i>
  </div>
</template>

<script>
import Base from '../../libs/base'

export default {
  name: 'x-progress',
  mixins: [Base],
  props: {
    percent: {
      type: Number,
      default: 0
    },
    showCancel: {
      type: Boolean,
      default: true
    }
  },
  methods: {
    cancel () {
      this.$emit('on-cancel')
    }
  }
}
</script>

<style lang="less">
@import '../../styles/weui/widget/weui_progress/weui_progress';
img{
  position: absolute;
  // margin-left: -30px;
  margin-top: -16px;
}
</style>
