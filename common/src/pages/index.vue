<template>
  <div class="news-box">
    <div class="scroll-container">
      <!-- 根据待显示新闻列表数组，显示新闻列表 -->
      <div v-for="(item, index) in allDataList" :key="index">
        <router-link
          class="one-new"
          :to=" '/article/' + item.title + '/'+ item.reads + '/'+ item.from + '/'+ item.date + '/'+ item.image "
        >
          <!-- 新闻左侧标题、评论、来源部分 -->
          <div class="new-left">
            <h3>{{ item.title }}</h3>
            <div>
              <p>
                <img src="../assets/icons/msg.png" alt="评" />
                <span>{{ item.reads }}</span>
                <span>{{ item.from }}</span>
              </p>
              <h4>{{ item.date }}</h4>
            </div>
          </div>
          <!-- 新闻右侧图片部分 -->
          <div class="new-right">
            <img :src="imgsList[item.image]" alt="PIC" />
          </div>
        </router-link>
      </div>
      <!-- 请求状态下 显示对应 msg 提示信息 -->
      <div v-if="isRequestStatus" class="msg">
        <h2>{{ msg }}</h2>
      </div>
    </div>
  </div>
</template>

<script>
// 引入准备好的新闻图片相关信息
import imgsList from "../components/newsImgs.js";
export default {
  data() {
    return {
      // 用来保存 所有列表元素
      allDataList: [],
      // 数据请求状态判断
      isRequestStatus: true,
      // 提示显示信息
      msg: "小二正在努力，请耐心等待...",
      // 图片数组
      imgsList
    };
  },
  async mounted() {
    // 分批发送请求时，先请求一部分数据保证数据显示
    let request = await this.getMock(10000);
    if (!!request && request.length > 0) {
      this.allDataList = [...request];
      this.isRequestStatus = false;
    }
  },
  methods: {
    // 发送请求获取新的请求模拟数据，这个是跨域请求的网络mock数据
    getMock(num) {
      this.isRequestStatus = true;
      this.msg = "小二正在努力，请耐心等待...";
      return this.$axios
        .get("http://localhost:4000/data?num=" + num)
        .then(res => {
          this.isRequestStatus = false;
          return res.data.list;
        })
        .catch(() => {
          this.msg = "亲，网络请求出错啦！赶快检查吧...";
          return false;
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.news-box {
  width: 100%;
  max-width: 800px;
  height: 100%;
  .scroll-container {
    width: 100%;
    height: 100%;
    .one-new {
      text-decoration: none;
      display: block;
      display: flex;
      flex-direction: row;
      flex-wrap: nowrap;
      justify-content: space-between;
      border-bottom: 1px solid #ddd;
      padding: 14px 10px 5px;
      .new-left {
        height: 80px;
        position: relative;
        h3 {
          padding: 0;
          margin: 0;
          font-size: 16px;
          text-align: justify;
          color: #555;
        }
        div {
          position: absolute;
          width: 100%;
          bottom: 10px;
          display: flex;
          flex-direction: row;
          flex-wrap: nowrap;
          justify-content: space-between;
          align-items: center;
          p {
            display: flex;
            flex-direction: row;
            flex-wrap: nowrap;
            justify-content: space-between;
            align-items: center;
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
          h4 {
            font-size: 12px;
            color: #888;
          }
        }
      }
      .new-right {
        margin-left: 10px;
        img {
          height: 68px;
        }
      }
    }
    .msg h2 {
      font-size: 18px;
      text-align: center;
      color: #666;
      padding-top: 58px;
    }
  }
}
</style>
