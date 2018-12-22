<template>
  <div class="goods-list">
    <!-- <router-link class="goods-item" v-for="item in goodslist" :key="item.id" :to="'/home/goodsinfo/' + item.id" tag="div">
      <img :src="item.img_url" alt="">
      <h1 class="title">{{ item.title }}</h1>
      <div class="info">
        <p class="price">
          <span class="now">￥{{ item.sell_price }}</span>
          <span class="old">￥{{ item.market_price }}</span>
        </p>
        <p class="sell">
          <span>热卖中</span>
          <span>剩{{ item.stock_quantity }}件</span>
        </p>
      </div>
    </router-link>-->
    <!-- 在网页中，有两种跳转方式： -->
    <!-- 方式1： 使用 a 标签 的形式叫做 标签跳转  -->
    <!-- 方式2： 使用 window.location.href 的形式，叫做 编程式导航 -->
    <div class="goods-item" v-for="item in goodslist" :key="item.id" @click="goDetail(item.id)">
      <img :src="item.img_url" alt>
      <h1 class="title">{{ item.title }}</h1>
      <div class="info">
        <p class="price">
          <span class="now">￥{{ item.sell_price }}</span>
          <span class="old">￥{{ item.market_price }}</span>
        </p>
        <p class="sell">
          <span>热卖中</span>
          <span>剩{{ item.stock_quantity }}件</span>
        </p>
      </div>
    </div>

    <mt-button type="danger" size="large" @click="getMore">加载更多</mt-button>
  </div>
</template>

<script>
export default {
  data() {
    // data 是往自己组件内部，挂载一些私有数据的
    return {
      pageindex: 1, // 分页的页数
      goodslist: [
        {
          img_url:
            "https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3193876497,1577091960&fm=26&gp=0.jpg",
          id: 0,
          title: "百度图片使用世界前沿的人",
          sell_price: 2199,
          market_price: "2499",
          stock_quantity: 50
        },
        {
          img_url:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=686793297,3976752776&fm=27&gp=0.jpg",
          id: 1,
          title: "百度图片使用世界前沿的人",
          sell_price: 2499,
          market_price: 2799,
          stock_quantity: 40
        },
        {
          img_url:
            "https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=2631790481,628199863&fm=173&app=49&f=JPEG?w=640&h=400&s=32A1D0034C270207308535200300A040",
          id: 2,
          title: "百度图片使用世界前沿的人",
          sell_price: 2099,
          market_price: 2799,
          stock_quantity: 43
        },
        {
          img_url:
            "https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=1666226745,1014906934&fm=173&app=49&f=JPEG?w=640&h=240&s=BA3361849F182E535E6619850300708B",
          id: 3,
          title: "百度图片使用世界前沿的人",
          sell_price: 2099,
          market_price: 2799,
          stock_quantity: 43
        },
        {
          img_url:
            "https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2613600636,2328272980&fm=26&gp=0.jpg",
          id: 4,
          title: "百度图片使用世界前沿的人",
          sell_price: 2099,
          market_price: 2799,
          stock_quantity: 43
        },
        {
          img_url:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=18177434,2294747453&fm=26&gp=0.jpg",
          id: 5,
          title: "百度图片使用世界前沿的人",
          sell_price: 2099,
          market_price: 2799,
          stock_quantity: 43
        },
        {
          img_url:
            "https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2397332000,1697881456&fm=26&gp=0.jpg",
          id: 6,
          title: "百度图片使用世界前沿的人",
          sell_price: 2099,
          market_price: 2799,
          stock_quantity: 43
        },
        {
          img_url:
            "https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1096220361,3162288618&fm=26&gp=0.jpg",
          id: 7,
          title: "百度图片使用世界前沿的人",
          sell_price: 2099,
          market_price: 2799,
          stock_quantity: 43
        },
        {
          img_url:
            "https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2613600636,2328272980&fm=26&gp=0.jpg",
          id: 8,
          title: "百度图片使用世界前沿的人",
          sell_price: 2099,
          market_price: 2799,
          stock_quantity: 43
        }
      ] 
    };
  },
  created() {
    this.getGoodsList();
  },
  methods: {
    getGoodsList() {
      // 获取商品列表
      this.$http
        .get("api/getgoods?pageindex=" + this.pageindex)
        .then(result => {
          if (result.body.status === 0) {
            // this.goodslist = result.body.message;
            this.goodslist = this.goodslist.concat(result.body.message);
          }
        });
    },
    getMore() {
      this.pageindex++;
      this.getGoodsList();
    },
    goDetail(id) {
      // 使用JS的形式进行路由导航

      // 注意： 一定要区分 this.$route 和 this.$router 这两个对象，
      // 其中： this.$route 是路由【参数对象】，所有路由中的参数， params, query 都属于它
      // 其中： this.$router 是一个路由【导航对象】，用它 可以方便的 使用 JS 代码，实现路由的 前进、后退、 跳转到新的 URL 地址

      // console.log(this);
      // 1. 最简单的
      // this.$router.push("/home/goodsinfo/" + id);
      // 2. 传递对象
      // this.$router.push({ path: "/home/goodsinfo/" + id });
      // 3. 传递命名的路由
      this.$router.push({ name: "goodsinfo", params: { id } });
    }
  }
};
</script>

<style lang="scss" scoped>
.goods-list {
  display: flex;
  flex-wrap: wrap;
  padding: 7px;
  justify-content: space-between;

  .goods-item {
    width: 49%;
    border: 1px solid #ccc;
    box-shadow: 0 0 8px #ccc;
    margin: 4px 0;
    padding: 2px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    min-height: 230px;
    img {
      width: 100%;
      min-height: 180px;
    }
    .title {
      font-size: 13px;
    }

    .info {
      background-color: #eee;
      p {
        margin: 0;
        padding: 5px;
      }
      .price {
        .now {
          color: red;
          font-weight: bold;
          font-size: 16px;
        }
        .old {
          text-decoration: line-through;
          font-size: 12px;
          margin-left: 10px;
        }
      }
      .sell {
        display: flex;
        justify-content: space-between;
        font-size: 13px;
      }
    }
  }
}
</style>

