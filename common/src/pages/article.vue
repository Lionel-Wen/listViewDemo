<template>
  <div class="container">
    <router-link to="/">
      <img src="../assets/icons/backward.png" alt="《《" />
      返回列表
    </router-link>
    <div class="content">
      <h2>{{ this.$route.params.title }}</h2>
      <p class="info">
        <img src="../assets/icons/msg.png" alt="评" />
        <span>{{ this.$route.params.reads }}</span>
        <span>{{ this.$route.params.from }}</span>
        <span>{{ this.$route.params.date }}</span>
      </p>
      <img :src="imgsList[this.$route.params.image]" alt />
      <p>这里是新闻详情页面...</p>
      <p>这里是新闻详情页面...</p>
      <img :src="imgsList[1]" alt />
      <p>这里是新闻详情页面...</p>
      <p>这里是新闻详情页面...</p>
      <img :src="imgsList[8]" alt />
      <p>这里是新闻详情页面...</p>
      <p>这里是新闻详情页面...</p>
      <img :src="imgsList[6]" alt />
      <img :src="imgsList[11]" alt />
      <p>这里是新闻详情页面...</p>
      <p>这里是新闻详情页面...</p>
    </div>
  </div>
</template>

<script>
// 引入准备好的新闻图片相关信息
import imgsList from "../components/newsImgs.js";
export default {
  data() {
    return {
      imgsList
    };
  }
};
</script>

<style lang="scss" scoped>
.container {
  width: 100%;
  max-width: 800px;
  padding-bottom: 60px;
  a {
    margin: 15px;
    text-decoration: none;
    color: #007cba;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: flex-start;
    align-items: center;
    img {
      height: 16px;
    }
  }
  .content {
    text-align: center;
    h2 {
      color: #555;
      font-size: 16px;
      text-align: center;
      margin: 10px 20px;
    }
    img {
      margin: 10px 0;
    }
    p {
      display: flex;
      flex-direction: row;
      flex-wrap: nowrap;
      justify-content: center;
      align-items: center;
      line-height: 28px;
      img {
        height: 16px;
      }
      span {
        font-size: 12px;
        color: #555;
        margin-left: 3px;
        margin-right: 3px;
      }
    }
    .info {
      margin: 5px 0 10px;
    }
    h4 {
      font-size: 12px;
      color: #888;
    }
  }
}
</style>
