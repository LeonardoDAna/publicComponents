<template>
  <!-- 天气和时钟展示插件 -->
  <div class="weatherAndClock row align-middle">
    <div class="timeBlock my-mr-10">{{ time }}</div>
    <div class="dateBlock my-mr-10">
      <div>{{ week }}</div>
      <div>{{ date }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "weatherAndClock",
  data() {
    return {
      time: "",
      date: "",
      week: "",
      timer: null,
    };
  },

  mounted() {
    this.getNowTime();
    this.timer = setInterval(this.getNowTime, 1000);
  },

  beforeDestroy() {
    clearInterval(this.timer);
  },
  methods: {
    addZero(val) {
      return val < 10 ? "0" + val : val;
    },

    // 把阿拉伯数字的星期转化为英文缩写
    trans(val) {
      let obj = ["周日", "周一", "周二", "周三", "周四", "周五", "周六"];
      return obj[val];
    },
    getNowTime() {
      let nowDate = new Date();
      let year = nowDate.getFullYear(); // 获取年
      let month = nowDate.getMonth() + 1; // 获取月（是从0到11，所以我们要给他加1）
      let date = nowDate.getDate(); // 获取日
      let day = nowDate.getDay(); // 获取星期几(0是星期日)
      let hour = nowDate.getHours(); // 获取小时
      let min = nowDate.getMinutes(); // 获取分钟
      let sec = nowDate.getSeconds(); // 获取秒

      this.time =
        this.addZero(hour) + ":" + this.addZero(min) + ":" + this.addZero(sec);
      this.date = year + ":" + this.addZero(month) + ":" + this.addZero(date);
      this.week = this.trans(day);
    },
  },
};
</script>

<style  lang="scss" scoped>
@import "@/styles/_handle.scss";
.weatherAndClock {
  @include font_color("headerColor_2");
}
.iconBlock {
  img {
    display: block;
    width: 1.83rem;
    height: 1.69rem;
  }
}
.timeBlock {
  line-height: 1;
  font-size: 2rem;
}
.dateBlock {
  font-size: 0.88rem;
}
</style>