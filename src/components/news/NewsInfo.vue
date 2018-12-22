<template>
  <div class="newsinfo-container">
    <!-- 大标题 -->
    <h3 class="title">{{ newsinfo.title }}</h3>
    <!-- 子标题 -->
    <p class="subtitle">
      <span>发表时间：{{ newsinfo.add_time | dateFormat }}</span>
      <span>点击：{{ newsinfo.click }}次</span>
    </p>

    <hr>

    <!-- 内容区域 -->
    <div class="content" v-html="newsinfo.content"></div>

    <!-- 评论子组件区域 -->
    <comment-box :id="this.id"></comment-box>
  </div>
</template>

<script>
// 1. 导入 评论子组件
import comment from "../subcomponents/comment.vue";

export default {
  data() {
    return {
      id: this.$route.params.id, // 将 URL 地址中传递过来的 Id值，挂载到 data上，方便以后调用
      newsinfo: {// 新闻对象
          "title":"柔性电子技术", 
          'add_time': "Wed Dec 13 2018 19:43:45 GMT+0800 (香港标准时间)",
          "click": 5, 
          "content":"<p>空客客舱将应用柔性电子技术</p><p>本报讯(记者 董禹含)如果飞机客舱座位上的显示屏都变为0.01毫米薄，不用时还能卷起来；甚至客舱的墙壁就是一块彩色柔性显示屏，实时显示着空中画面，<img src='https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=1607665642,3313324910&fm=173&app=49&f=JPEG?w=640&h=480&s=5F12E409D39463C4673335D6030010AA'>会给旅客带来怎样的体验？日前，空中客车中国创新中心与柔宇科技有限公司签署合作备忘录，双方将就柔性电子技术在飞机客舱的应用和商业合作开展研究。</p>"
      } 
    };
  },
  created() {
    this.getNewsInfo();
  },
  methods: {
    getNewsInfo() {
      // 获取新闻详情
      this.$http.get("api/getnew/" + this.id).then(result => {
        if (result.body.status === 0) {
          this.newsinfo = result.body.message[0];
        } else {
          Toast("获取新闻失败！");
        }
      });
    }
  },
  components: {
    // 用来注册子组件的节点
    "comment-box": comment
  }
};
</script>

<style lang="scss">
.newsinfo-container {
  padding: 0 4px;
  .title {
    font-size: 16px;
    text-align: center;
    margin: 15px 0;
    color: red;
  }
  .subtitle {
    font-size: 13px;
    color: #226aff;
    display: flex;
    justify-content: space-between;
  }
  .content {
    img {
      width: 100%;
    }
  }
}
</style>
