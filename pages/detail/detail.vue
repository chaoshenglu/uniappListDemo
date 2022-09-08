<template>
  <view style="display: flex;flex-direction: column;justify-content: center;align-items: center;">
    <text>{{id}}</text>
    <button>测试修改</button>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        id: null
      }
    },
    onLoad(option) {
      this.id = option.id
    },
    methods: {

    }
  }
</script>

<style>

</style>
