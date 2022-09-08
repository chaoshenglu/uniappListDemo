<script>
  export default {
    onLaunch: function() {
      console.log('App Launch')
    },
    onShow: function() {
      console.log('App Show')
    },
    onHide: function() {
      console.log('App Hide')
    },
    methods: {
      get(uri, param) {
        let baseUrl = 'https://www.fastmock.site/mock/8bd64be11a7822b9df73f824e263a142/api/'
        let url = baseUrl + uri
        console.log('🔽网络请求POST=>', url)
        console.log('参数=>', JSON.stringify(param))
        let promise = new Promise(function(resolve, reject) {
          uni.request({
            url: url,
            data: param,
            method: 'GET',
            success: res => {
              console.log(uri, '🔼️接口返回=>', res.data)
              resolve(res.data)
            },
            fail: err => {
              console.log(uri, '🔼️请求失败=>', err)
              reject(err)
            }
          })
        })
        return promise
      },
    }
  }
</script>

<style lang="scss">
  @import "@/uni_modules/uview-ui/index.scss";
</style>
