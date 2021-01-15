<template>

  <swiper class="detail-swiper">
    <swiper-item class="swiper-item" v-for="item in topImages">
      <img :src="item" alt="" @load="imageLoad">
    </swiper-item>
  </swiper>

</template>

<script>
  import {Swiper, SwiperItem} from 'components/common/swiper'

  export default {
    name: "DetailSwiper",
    components: {
      Swiper,
      SwiperItem
    },
    data(){
      return {
        isLoad: false
      }
    },
    props: {
      topImages: {
        type: Array,
        default() {
          return []
        }
      }
    },
    methods: {
      imageLoad() {
        if(!this.isLoad){
          this.$emit('detailSwiperImageLoad')
          this.isLoad = true
        }
      }
    }
  }
</script>

<style scoped>
.detail-swiper {
  height: 300px;
}
</style>
