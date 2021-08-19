<template>
  <div id="app">
    <!-- 路由放置区域，keep-alive目的是为了确保在路由切换的过程中缓存一定的关键数据 -->
    <div class="router" :style="{ height : windowHeight+'px' }">
      <keep-alive>
        <router-view></router-view>
      </keep-alive>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      //整个可视窗口的高度
      windowHeight: 0
    };
  },
  computed: {},
  mounted() {
    // 初始化窗口的高度并监测屏幕变化及手机横竖屏变化事件，准确的拿到对应的容器内部可显示区域的大小
    this.windowHeight = window.innerHeight;
    window.onresize = this.myresize;
    window.orientationchange = this.myresize;
  },
  methods: {
    myresize: () => {
      this.windowHeight = window.innerHeight;
    }
  }
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}
html,
body {
  background-color: #efefef;
  height: 100%;
  width: 100%;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>