<template>
 <div class="goods-params" v-if="Object.keys(goodsInfo).length !== 0">

   <div class="params-size">
     <table class="size-table">
       <tr class="size-table-row" v-for="(item, index) in goodsInfo.sizes[0]">
         <td v-for="(item_inside, index_inside) in item">
           {{item_inside}}
         </td>
       </tr>
     </table>
   </div>

   <div class="params-info">
     <table class="size-table">
       <tr class="size-table-row" v-for="(item, index) in goodsInfo.infos">
         <td class="key">{{item.key}}</td>
         <td class="value">{{item.value}}</td>
       </tr>
     </table>
   </div>

   <div class="params-image" v-if="goodsInfo.image.length !== 0">
     <img :src="goodsInfo.image" alt="">
   </div>

 </div>
</template>

<script>
  export default {
    name: "DetailGoodsParams",
    data() {
      return {
        sizes: []
      }
    },
    props: {
      goodsInfo: {
        type: Object,
        default() {
          return {}
        }
      }
    },


  }
</script>

<style scoped>
  .params-size{
    margin-top: 20px;
    /*margin-left: 25px;*/
    /*margin-right: 15px;*/
    font-size: 14px;
    /*width: 100%;*/
    border-bottom: #f2f5f8 solid 3px;
  }

  .size-table {
    width: 100%;
    margin-left: 25px;
    margin-right: 40px;
    border-collapse: collapse;
  }

  .params-size table tr {
    display: flex;
    height: 45px;
    /*margin-right: 50px;*/
    border-bottom: solid 1px rgba(100,100,100,.1);
    justify-content:center;
    align-items:center;

  }

  .size-table-row td {
    flex: 1;
  }
  /* 下面是第二张表 */
  .params-info{
    /*margin-top: 20px;*/
    /*margin-left: 25px;*/
    /*margin-right: 15px;*/
    font-size: 14px;
    /*width: 100%;*/
    border-bottom: #f2f5f8 solid 3px;
  }

  .params-info table tr{
    height: 45px;
    border-bottom: solid 1px rgba(100,100,100,.1);
  }

  .key {
    width: 80px;
  }

  .value {
    color: var(--color-high-text);
  }

  .params-image img {
    width: 100%;
  }
</style>
