<template>
  <div class="main">
      <a-button :style="`float: right;`" size="large" type="primary" @click="getYzmCode">
      <span v-show="showObtainCode">{{ obtainCode }}</span>
      <span v-show="!showObtainCode">
        <CountDown
          ref="countDownRef"
          :showMin="showMin"
          :showSec="showSec"
          :min="0"
          :sec="60"
          :countStyle="'color: #fff;font-size: 14px;'"
          @finishCountDown="finishCountDown"
          @finishMinutes="finishMinutes"
        />
      </span>
      <span style="font-size: 14px" v-show="!showObtainCode">{{ `${showMin ? '分钟' : 's'}后重新获取` }}</span>
    </a-button>
  </div>
</template>

<script>
import CountDown from '@/myComponents/CountDown/CountDown.vue'

export default {
  name: 'FirstLogin',
  components: {
    CountDown,
  },
  data() {
    return {
      phoneNum: '',
      obtainCode: '获取验证码',
      showMin: false,
      showSec: true,
      showObtainCode: true,
    }
  },
  mounted() {x},
  created() {},
  methods: {
    startCount() {
      this.$refs.countDownRef.startCountDown()
    },
    finishCountDown() {
      console.log('倒计时完成')
      this.showObtainCode = true
    },
    finishMinutes() {
      console.log('分钟倒计时完成')
      this.showMin = false
      this.showSec = true
    },
    getYzmCode() {
      if (!/^1(3|4|5|6|7|8|9)\d{9}$/.test(this.phoneNum)) {
        this.$message.error('手机号码有误，请重填')
        return
      }
      /**验证码一分钟以上 */
      // this.showMin = true
      // this.showSec = false
      // this.showObtainCode = false
      /**验证码一分钟以内 */
      this.showMin = false
      this.showSec = true
      this.showObtainCode = false
      this.startCount()
    },
  },
}
</script>

<style>
</style>