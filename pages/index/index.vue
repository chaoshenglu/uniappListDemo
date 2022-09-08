<template>
  <view style="display: flex;flex-direction: column;align-items: center;">
    <view class="listCell" v-for="(item,index) in list" :key="index">
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        list: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
      }
    },
    onLoad() {
      this.requestData()
    },
    methods: {
      requestData() {
        let uri = 'listByPage'
        getApp().get(uri, {
          page: 1
        }).then(res => {

        }).catch(err => {
          console.log(err)
        })
      }
    }
  }
</script>

<style lang="scss">
  page {
    padding-bottom: 50px;
  }

  .listCell {
    background-color: white;
    width: 84vw;
    border-radius: 10px;
    padding-left: 4vw;
    padding-right: 4vw;
    padding-top: 10px;
    padding-bottom: 10px;
    box-shadow: 0px 0px 4px 4px rgba(0, 0, 0, 0.04);
    margin-top: 16px;
    min-height: 40px;
  }
</style>
