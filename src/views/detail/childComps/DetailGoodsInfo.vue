<template>
  <div v-if="Object.keys(detailInfo).length !== 0" class="detail-goods-info">
    <div class="goodsinfo-desc">
      <div class="start"></div>
      <div class="desc">{{detailInfo.desc}}</div>
      <div class="end"></div>
    </div>

    <div>
      <div class="info-key">{{detailInfo.detailImage[0].key}}</div>
      <div class="info-list">
        <img v-for="(item, index) in detailInfo.detailImage[0].list" :src="item" alt="" @load="imageLoadfinish">
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "DetailGoodsInfo",
    props: {
      detailInfo: {
        type: Object,
        default() {
          return {}
        }
      }
    },
    methods: {
      imageLoadfinish() {
        this.$emit('imageLoadfinish')
      }
    }
  }
</script>

<style scoped>
  .detail-goods-info {
    margin-top: 20px;
    border-bottom: 5px solid #f2f5f8;
  }

  .goodsinfo-desc {
    padding: 0 15px;
  }

  .goodsinfo-desc .start, .goodsinfo-desc .end {
    width: 90px;
    height: 1px;
    background-color: #a3a3a5;
    position: relative;
  }

  .goodsinfo-desc .start {
    float: left;
  }

  .goodsinfo-desc .end {
    float: right;
  }

  .goodsinfo-desc .start::before, .goodsinfo-desc .end::after {
    content: '';
    position: absolute;
    width: 5px;
    height: 5px;
    background-color: #333;
    bottom: 0;
  }

  .goodsinfo-desc .end::after {
    right: 0;
  }

  .goodsinfo-desc .desc {
    padding: 15px 0;
    font-size: 14px;
  }

  .info-key {
    margin: 10px 0 10px 15px;
    color: #333;
    font-size: 15px;
  }

  .info-list img {
    width: 100%;
  }
</style>
