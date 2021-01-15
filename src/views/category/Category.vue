<template>
  <div class="wrapper">
    <ul class="content">
      <li>xxxxx</li>
      <li>xxxxx1</li>
      <li>xxxxx2</li>
      <li>xxxxx3</li>
      <li>xxxxx4</li>
      <li>xxxxx5</li>
      <li>xxxxx6</li>
      <li>xxxxx7</li>
      <li>xxxxx8</li>
      <li>xxxxx9</li>
      <li>xxxxx10</li>
    </ul>
  </div>

</template>

<script>
  import BScroll from '@better-scroll/core'


  export default {
    name: "Category",
    data() {
      return {
        scroll: null
      }
    },
    mounted() {
      this.scroll = new BScroll('.wrapper', {

      })
      console.log(this.scroll);
    }
  }
</script>

<style scoped>
  .wrapper {
    height: 100px;
    background-color: greenyellow;
  }
</style>
