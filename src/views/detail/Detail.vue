<template>
  <div id="detail">
    <detail-nav-bar class="detail-nav"></detail-nav-bar>
    <scroll class="content" ref="detail_scroll">
      <detail-swiper :top-images="topImages" @detailSwiperImageLoad="detailSwiperImageLoad"></detail-swiper>
      <detail-base-info :goods="goods"></detail-base-info>
      <detail-shop-info :shop="shop"></detail-shop-info>
      <detail-goods-info :detailInfo="detailInfo" @imageLoadfinish="imageLoadfinish"></detail-goods-info>
      <detail-goods-params :goodsInfo="goodsInfo"></detail-goods-params>
      <detail-comment-info :commentInfo="commentInfo"></detail-comment-info>
    </scroll>
  </div>
</template>

<script>
  import DetailNavBar from "./childComps/DetailNavBar";
  import DetailSwiper from "./childComps/DetailSwiper";
  import DetailBaseInfo from "./childComps/DetailBaseInfo";
  import DetailShopInfo from "./childComps/DetailShopInfo";
  import DetailGoodsInfo from "./childComps/DetailGoodsInfo";
  import DetailGoodsParams from "./childComps/DetailGoodsParams";
  import DetailCommentInfo from "./childComps/DetailCommentInfo"

  import Scroll from 'components/common/scroll/Scroll'

  import {getDetail, Goods, Shop, GoodsParam} from 'network/detail'
  import {debounce} from 'common/utils'


  export default {
    name: "Detail",
    data() {
      return {
        iid: null,
        topImages: [],
        goods: {},
        shop: {},
        detailInfo: {},
        goodsInfo: {},
        commentInfo: {},
        refresh: null
      }
    },
    components: {
      DetailNavBar,
      DetailSwiper,
      DetailBaseInfo,
      DetailShopInfo,
      DetailGoodsInfo,
      DetailGoodsParams,
      DetailCommentInfo,
      Scroll
    },
    created() {
      // 1. 保存传入的iid
      this.iid = this.$route.params.iid

      // 2. 根据iid请求详情数据
      getDetail(this.iid).then(res => {
        console.log(res);
        // 1. 获取顶部图片
        this.topImages = res.result.itemInfo.topImages

        // 2. 获取商品信息
        this.goods = new Goods(res.result.itemInfo, res.result.columns, res.result.shopInfo.services)

        // 3. 获取店铺信息
        this.shop = new Shop(res.result.shopInfo)

        // 4. 保存商品的详情数据
        this.detailInfo = res.result.detailInfo

        // 5. 保存商品的参数列表
        this.goodsInfo = new GoodsParam(res.result.itemParams.info, res.result.itemParams.rule)

        // 6. 获取评论信息
        if(res.result.rate.cRate !== 0) {
          this.commentInfo = res.result.rate.list[0]
        }
      })

    },
    mounted() {
      // 1. 图片加载完成的事件监听
      this.refresh = debounce(this.$refs.detail_scroll.refresh, 50)

    },
    methods: {
      detailSwiperImageLoad() {
        this.$refs.detail_scroll.refresh()
      },
      imageLoadfinish() {
        this.refresh()
      }
    }
  }
</script>

<style scoped>
  #detail{
    position: relative;
    z-index: 10;
    background-color: #fff;
    height: 100vh;
  }

  .content {
    height: calc(100% - 44px)
  }

  .detail-nav {
    position: relative;
    z-index: 9;
    background-color: #fff;
  }
</style>
