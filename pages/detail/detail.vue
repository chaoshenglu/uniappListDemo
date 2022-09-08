<template>
  <view>
    <view class="box">
      <text>{{page}}-{{id}}</text>
      <button style="margin-top: 40px;">测试修改</button>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        id: null,
        page: null
      }
    },
    onLoad(option) {
      this.id = option.id
      this.page = option.page
    },
    methods: {

    }
  }
</script>

<style lang="scss">
  .box {
    width: 100vw;
    height: 200px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
</style>
