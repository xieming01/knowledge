<template>
  <div class="goodsdesc-container">
    <h3>{{ info.title }}</h3>

    <hr>

    <div class="content" v-html="info.content"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      info: {
        "title":"叙利亚局势将进入新阶段",
        "content":"<p>空客客舱将应用柔性电子技术</p><p>本报讯(记者 董禹含)如果飞机客舱座位上的显示屏都变为0.01毫米薄，不用时还能卷起来；甚至客舱的墙壁就是一块彩色柔性显示屏，实时显示着空中画面，会给旅客带来怎样的体验？日前，空中客车中国创新中心与柔宇科技有限公司签署合作备忘录，双方将就柔性电子技术在飞机客舱的应用和商业合作开展研究。</p>"
      } // 图文数据
    };
  },
  created() {
    this.getGoodsDesc();
  },
  methods: {
    getGoodsDesc() {
      this.$http
        .get("api/goods/getdesc/" + this.$route.params.id)
        .then(result => {
          if (result.body.status === 0) {
            this.info = result.body.message[0];
          }
        });
    }
  }
};
</script>

<style lang="scss">
.goodsdesc-container {
  padding: 4px;
  h3 {
    font-size: 16px;
    color: #226aff;
    text-align: center;
    margin: 15px 0;
  }
  .content{
    img{
      width: 100%;
    }
  }
}
</style>
