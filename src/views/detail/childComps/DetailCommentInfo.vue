<template>
  <div class="comment-info" v-if="Object.keys(commentInfo).length !== 0">
    <div class="tips">
      <span>用户评价</span>
      <span class="tips-text">
        更多
        <img src="~assets/img/detail/right.svg" alt="">
      </span>
    </div>
    <div class="comment-info-top">
      <img :src="commentInfo.user.avatar" alt="">
      <span>{{commentInfo.user.uname}}</span>
    </div>

    <div class="comment-info-middle">
      <span>{{commentInfo.content}}</span>
    </div>

    <div class="comment-info-bottom">
      <span>{{commentInfo.created | showDate}}</span>
      <span class="size">{{commentInfo.style}}</span>
    </div>
  </div>
</template>

<script>
  export default {
    name: "DetailCommentInfo",
    props: {
      commentInfo: {
        type: Object,
        default() {
          return {}
        }
      }
    },
    filters: {
      showDate(value) {
        // 1.
      }
    }
  }
</script>

<style scoped>
  .comment-info {
    border-bottom: #f2f5f8 solid 5px;
  }

  .tips {
    height: 40px;
    margin: 20px 20px 0 20px;
    font-size: 15px;
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-between;
    border-bottom: 1px solid rgba(100,100,100,.1);
  }

  .tips .tips-text {
    font-size: 14px;
  }

  .tips span img {
    height: 13px;
    width: 13px;
  }

  .comment-info-top {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    margin-left: 20px;
    margin-top: 10px;
  }

  .comment-info-top img {
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }

  .comment-info-top span {
    margin-left: 10px;
    font-size: 15px;
  }

  .comment-info-middle {
    line-height: 22px;
    margin: 10px 20px;
    font-size: 13px;
    color: var(--color-text)
  }

  .comment-info-bottom {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    margin-left: 20px;
    margin-top: 10px;
    font-size: 12px;
    color: #999;
    margin-bottom: 20px;
  }

  .comment-info-bottom .size {
    margin-left: 10px;
  }
</style>
