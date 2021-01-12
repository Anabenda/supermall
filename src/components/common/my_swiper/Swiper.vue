<template>
  <!-- 轮播图最外层div  -->
  <div class="hy-swiper">
    <div class="swiper">
      <!-- 预留给图片的位置 -->
      <slot></slot>
    </div>
    <!-- 预留给显示小圆点的位置 -->
    <slot name="indicator"></slot>
    <div class="indicator">
      <!-- 小圆点的位置  -->
      <slot name="indicator" v-if="showIndicator && swiperCount > 1">
        <div v-for="(item, index) in swiperCount" class="indi-item" :class="{active: index === currentIndex - 1}" :key="index"></div>
      </slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "Swiper",
  props: {
    interval: { // 轮换间隔
      type: Number,
      default: 3000
    },
    animDuration: { // 轮换持续时长
      type: Number,
      default: 300
    },
    moveRatio: { // finger滑到多少比例切换下一张
      type: Number,
      default: .25
    },
    showIndicator: { // 是否要小圆点
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      swiperCount: 0,  // 图片个数
      totalWidth: 0, // 整个swiper的宽度
      swiperStyle: {}, // 样式
      currentIndex: 1, // 当前索引
      scrolling: false // 当前是否在滚动
    }
  },
  mounted() {
    // 初始化一些东西
    // 1. 操作dom，在前后添加slide
    setTimeout(() => {
      this.handleDom()

      // 2. 开启定时器
      this.startTimer()
    }, 3000)
  },
  methods: {
    /**
     * 定时器操作
     * */
    startTimer() {
      this.loopTime = window.setInterval(() => {
        // 每interval个时间执行一次
        this.currentIndex ++
        this.scrollContent(-this.currentIndex * this.totalWidth)
      }, this.interval)
    },
    /**
     * 操作dom，在dom前后添加slide
     */
    handleDom() {
      // 1. 获取要添加的元素
      let swiperEL = document.querySelector('.swiper')  // 获取它的css属性
      let slidesELs = swiperEL.getElementsByClassName('slide')

      // 2. 保存个数
      this.slideCount = slidesELs.length

      // 3. 大于一个，则在左右添加<   >
      if(this.slideCount > 1) {
        //
        let cloneFirst = slidesELs[0].cloneNode(true)
        let cloneLast = slidesELs[this.slideCount - 1].cloneNode(true)

        // 把节点都连起来
        swiperEL.insertBefore(cloneLast, slidesELs[0])
        swiperEL.appendChild(cloneFirst)
        this.totalWidth = swiperEL.offsetWidth
        this.swiperStyle = swiperEL.style
      }
    },
    /**
     * 滚动到正确的位置
     * @param currentPosition
     */
    scrollContent(currentPosition) {
      // 1. 设置正在滚动属性
      this.scrolling = true

      // 2. 开启滚动动画
      this.swiperStyle.transition = 'transform ' + this.animDuration + 'ms'
      this.setTransform(currentPosition);

      // 3.判断滚动到的位置
      this.checkPosition();

      // 4.滚动完成
      this.scrolling = false
    },

    /**
     * 设置滚动的位置
     */
    setTransform: function (position) {
      this.swiperStyle.transform = `translate3d(${position}px, 0, 0)`;
      this.swiperStyle['-webkit-transform'] = `translate3d(${position}px), 0, 0`;
      this.swiperStyle['-ms-transform'] = `translate3d(${position}px), 0, 0`;
    },
    /**
     * 校验正确的位置
     */
    checkPosition: function () {
      window.setTimeout(() => {
        // 1.校验正确的位置
        this.swiperStyle.transition = '0ms';
        if (this.currentIndex >= this.slideCount + 1) {
          this.currentIndex = 1;
          this.setTransform(-this.currentIndex * this.totalWidth);
        } else if (this.currentIndex <= 0) {
          this.currentIndex = this.slideCount;
          this.setTransform(-this.currentIndex * this.totalWidth);
        }

        // 2.结束移动后的回调
        this.$emit('transitionEnd', this.currentIndex-1);
      }, this.animDuration)
    },
  }
}
</script>

<style scoped>
  #hy-swiper {
    overflow: hidden;  /* 超出范围的内容会被修剪，并且其余内容是不可见的。 */
    position: relative;
  }

  .swiper {
    display: flex;
  }

  .indicator {
    display: flex;
    justify-content: center;
    position: absolute;
    width: 100%;
    bottom: 8px;
  }

  .indi-item {
    box-sizing: border-box;
    width: 8px;
    height: 8px;
    border-radius: 4px;
    background-color: #fff;
    line-height: 8px;
    text-align: center;
    font-size: 12px;
    margin: 0 5px;
  }

  .indi-item.active {
    background-color: rgba(212,62,46,1.0);
  }
</style>
