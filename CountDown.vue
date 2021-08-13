<template>
  <div :style="countStyle">
    <span v-if="showMin">{{ minute }}</span>
    <span v-if="showMin && showSec">:</span>
    <span v-if="showSec">{{ second }}</span>
  </div>
</template>

<script>
export default {
  name: 'CountDown',
  components: {},
  props: {
    showMin: Boolean,
    showSec: Boolean,
    min: Number,
    sec: Number,
    countStyle: String,
  },
  data() {
    return {
      // minutes: this.min,
      // seconds: 0,
      minutes: this.min,
      seconds: this.sec,
    }
  },
  computed: {
    second: function () {
      return this.num(this.seconds)
    },
    minute: function () {
      return this.num(this.minutes)
    },
  },
  watch: {
    second: {
      handler(newVal) {
        this.num(newVal)
      },
    },
    minute: {
      handler(newVal) {
        this.num(newVal)
      },
    },
  },
  mounted() {},
  created() {},
  methods: {
    num: function (n) {
      // return n < 10 ? '0' + n : '' + n
      return n
    },
    startCountDown() {
      var _this = this
      var time = window.setInterval(function () {
        if (_this.minutes == 1 && _this.seconds == 0) {
          console.log('%c%s', 'color: #86bf60;font-size: 18px;', _this.minutes, _this.seconds)
          _this.seconds = 60
          _this.minutes -= 1
          this.showMin = false
          this.showSec = true
        }
        if (_this.seconds === 0 && _this.minutes !== 0) {
          _this.seconds = 60
          _this.minutes -= 1
        } else if (_this.minutes === 0 && _this.seconds === 0) {
          // _this.seconds = 0
          _this.minutes = _this.min
          _this.seconds = _this.sec
          _this.$emit('finishCountDown')
          window.clearInterval(time)
          // console.log(_this.min);
          _this.minutes = _this.min
        } else if (_this.minutes === 0 && _this.seconds !== 0) {
            _this.$emit('finishMinutes')
            _this.seconds -= 1
        } else {
          _this.seconds -= 1
        }
      }, 1000)
    },
  },
}
</script>

<style lang='less' scoped>
</style>