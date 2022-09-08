<template>
  <view style="display: flex;flex-direction: column;align-items: center;">
    <view class="listCell" v-for="(item,index) in list" :key="index">
      <text>第{{item.page}}页 第{{item.id}}个</text>
    </view>
    <u-loadmore :status="status" />
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
    },

    onReachBottom() {
      this.page = this.page + 1
      if (this.page === 4) {
        this.status = 'nomore'
        return
      }
      this.requestData()
    },

    methods: {
      requestData() {
        this.status = 'loading'
        getApp().get('listByPage', {
          page: this.page
        }).then(res => {
          let list = res.data.list || []
          if (this.page === 1) {
            this.list = list
            this.status = 'loading'
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
