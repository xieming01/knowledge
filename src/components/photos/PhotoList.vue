<template>
  <div>
    
    <!-- 顶部滑动条区域 -->
    <div id="slider" class="mui-slider">
      <div id="sliderSegmentedControl" class="mui-scroll-wrapper mui-slider-indicator mui-segmented-control mui-segmented-control-inverted">
        <div class="mui-scroll">
          <a :class="['mui-control-item', item.id == 0 ? 'mui-active' : '']" v-for="item in cates" :key="item.id" @tap="getPhotoListByCateId(item.id)">
            {{ item.title }}
          </a>
        </div>
      </div>

    </div>

    <!-- 图片列表区域 -->
    <ul class="photo-list">
      <router-link v-for="item in list" :key="item.id" :to="'/home/photoinfo/' + item.id" tag="li">
        <img v-lazy="item.img_url">
        <div class="info">
          <h1 class="info-title">{{ item.title }}</h1>
          <div class="info-body">{{ item.zhaiyao }}</div>
        </div>
      </router-link>
    </ul>

  </div>
</template>

<script>
// 1. 导入 mui 的js文件
import mui from "../../lib/mui/js/mui.min.js";

export default {
  data() {
    return {
      cates: [// 所有分类的列表数组
        {"id": 0,"title": "全部"},
        {"id": 1,"title": "鹏城"},
        {"id": 2,"title": "网络"},
        {"id": 3,"title": "技术"},
        {"id": 4,"title": "智能"},
        {"id": 5,"title": "产业"},
        {"id": 6,"title": "战略"},
        {"id": 7,"title": "科学"},
      ], 
      list: [// 图片列表的数组
        { 
         "id": 0, 
         "img_url": "https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=385637348,2853520752&fm=173&app=25&f=JPG?w=218&h=146&s=0D408B468BECBE4D48ED11160300C0C2",
         "title":" 以下信息根据您的兴趣推荐锋网AI最佳掘金案例揭晓",
         "zhaiyao":"在8个被体验的服务行业中，快递、证券行业客服人员在服务规范方面相对较差。",
        },
        { 
         "id": 1, 
         "img_url": "https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=1524574992,3213241209&fm=173&app=49&f=JPEG?w=218&h=146&s=98E2ED130035E382C07174F50300C022",
         "title":" 以下信息根据您的兴趣推荐锋网AI最佳掘金案例揭晓",
         "zhaiyao":"在8个被体验的服务行业中，快递、证券行业客服人员在服务规范方面相对较差。",
        },
        { 
         "id": 2, 
         "img_url": "https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=3245602385,1839107893&fm=173&app=49&f=JPEG?w=218&h=146&s=EE24CC4B5CE0253E5F2475B80300C013",
         "title":" 以下信息根据您的兴趣推荐锋网AI最佳掘金案例揭晓",
         "zhaiyao":"在8个被体验的服务行业中，快递、证券行业客服人员在服务规范方面相对较差。",
        },
        { 
         "id": 3, 
         "img_url": "https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=3207594609,3658944537&fm=173&app=49&f=JPEG?w=218&h=146&s=2BE6722253C3B8A37B9D30DB0100E0A1",
         "title":" 以下信息根据您的兴趣推荐锋网AI最佳掘金案例揭晓",
         "zhaiyao":"在8个被体验的服务行业中，快递、证券行业客服人员在服务规范方面相对较差。",
        }
      ] 
    };
  },
  created() {
    this.getAllCategory();
    // 默认进入页面，就主动请求 所有图片列表的数据
    this.getPhotoListByCateId(0);
  },
  mounted() {
    // 当 组件中的DOM结构被渲染好并放到页面中后，会执行这个 钩子函数
    // 如果要操作元素了，最好在 mounted 里面，因为，这里时候的 DOM 元素 是最新的
    // 2. 初始化滑动控件
    mui(".mui-scroll-wrapper").scroll({
      deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
    });
  },
  methods: {
    getAllCategory() {
      // 获取所有的图片分类
      this.$http.get("api/getimgcategory").then(result => {
        if (result.body.status === 0) {
          // 手动拼接出一个最完整的 分类列表
          result.body.message.unshift({ title: "全部", id: 0 });
          this.cates = result.body.message;
        }
      });
    },
    getPhotoListByCateId(cateId) {
      // 根据 分类Id，获取图片列表
      this.$http.get("api/getimages/" + cateId).then(result => {
        if (result.body.status === 0) {
          this.list = result.body.message;
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
* {
  touch-action: pan-y;
}

.photo-list {
  list-style: none;
  margin: 0;
  padding: 10px;
  padding-bottom: 0;
  li {
    background-color: #ccc;
    text-align: center;
    margin-bottom: 10px;
    box-shadow: 0 0 9px #999;
    position: relative;
    img {
      width: 100%;
      vertical-align: middle;
    }
    img[lazy="loading"] {
      width: 40px;
      height: 300px;
      margin: auto;
    }

    .info {
      color: white;
      text-align: left;
      position: absolute;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.4);
      max-height: 84px;
      .info-title {
        font-size: 14px;
      }
      .info-body {
        font-size: 13px;
      }
    }
  }
}
</style>
