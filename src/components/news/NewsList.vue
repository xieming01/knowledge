<template>
  <div>
    <ul class="mui-table-view">
      <li class="mui-table-view-cell mui-media" v-for="item in newslist" :key="item.id">
        <router-link :to="'/home/newsinfo/' + item.id">
          <img class="mui-media-object mui-pull-left" :src="item.img_url">
          <div class="mui-media-body">
            <h1>{{ item.title }}</h1>
            <p class="mui-ellipsis">
              <span>发表时间：{{ item.add_time | dateFormat }}</span>
              <span>点击：{{item.click}}次</span>
            </p>
          </div>
        </router-link>
      </li>
    </ul>
  </div>
</template>
<script>
import { Toast } from "mint-ui";
import moment from 'moment'
export default {
  data() {
    return {
      newslist: [// 新闻列表
        {
          id: 0,
          img_url:"https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=3559966400,3263906468&fm=173&app=25&f=JPEG?w=218&h=146&s=C7B635C504423F470400808303006093",
          title: "14位民营企业家入选改革先锋",
          add_time: moment(),
          click: 1
        },
        {
          id: 2,
          img_url:"https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=3365209608,2269660351&fm=173&app=25&f=JPEG?w=218&h=146&s=0151AB6E9C691A9C8500351803001093",
          title: "长期暴跌的加密市场正在“吓跑”机构投资者",
          add_time: moment(),
          click: 2
        },
        {
          id: 3,
          img_url:"https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=393076525,4012519430&fm=173&app=25&f=JPEG?w=218&h=146&s=B52063B50A464ECC00A5555D030050E0",
          title: "菏泽取消楼市限售是怎么回事？菏泽取消楼市限售详细解读",
          add_time: moment(),
          click: 3
        }
      ]
    };
  },
  created() {
    this.getNewsList();
  },
  methods: {
    getNewsList() {
      // 获取新闻列表
      this.$http.get("api/getnewslist").then(result => {
        if (result.body.status === 0) {
          // 如果没有失败，应该把数据保存到 data 上
          this.newslist = result.body.message;
        } else {
          Toast("获取新闻列表失败！");
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.mui-table-view {
  li {
    h1 {
      font-size: 14px;
    }
    .mui-ellipsis {
      font-size: 12px;
      color: #226aff;
      display: flex;
      justify-content: space-between;
    }
  }
}
</style>
