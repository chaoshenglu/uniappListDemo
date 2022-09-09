<template>
  <view style="display: flex;flex-direction: column;align-items: center;">
    <view class="listCell" v-for="(item,index) in list" :key="index" @click="tapCell(item)">
      <text>第{{item.page}}页 第{{item.id}}个</text>
      <text v-if="item.didEdit">已修改</text>
    </view>
    <u-loadmore v-if="list && list.length > 0" :status="status" :line="true" marginTop="20" />
    <u-empty v-if="list && list.length === 0" icon="/static/empty.png" marginTop="150" />
  </view>
</template>

<script>
  export default {
    data() {
      return {
        list: [],
        page: 1,
        status: 'loadmore',
      }
    },

    onLoad() {
      this.page = 1
      this.requestData()
      uni.$on('testEdit', data => {
        for (let item of this.list) {
          if (`${item.page}` === `${data.page}` && `${item.id}` === `${data.id}`) {
            item.didEdit = true
          }
        }
        this.$forceUpdate()
      })
    },

    onUnload() {
      uni.$off('testEdit')
    },

    onPullDownRefresh() {
      this.page = 1
      this.requestData()
      setTimeout(function() {
        uni.stopPullDownRefresh()
      }, 1000)
    },

    onReachBottom() {
      if (this.status === 'nomore') {
        return
      }
      this.page = this.page + 1
      this.requestData()
    },

    methods: {

      tapCell(item) {
        uni.navigateTo({
          url: `/pages/detail/detail?id=${item.id}&page=${item.page}`
        })
      },

      requestData() {
        this.status = 'loading'
        getApp().get('listByPage', {
          page: this.page
        }).then(res => {
          let list = res.data.list || []
          if (this.page === 1) {
            this.list = list
            if (list.length < 10) {
              this.status = 'nomore'
            } else {
              this.status = 'loading'
            }
          } else {
            this.list = this.list.concat(list)
            if (list.length < 10) {
              this.status = 'nomore'
            } else {
              this.status = 'loading'
            }
          }
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
    background-color: #F8F8F8;
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
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
</style>
