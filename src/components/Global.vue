<template>
  <div class="global">
    <div class="error" v-if="error">
      <div class="error-msg-wrapper">
        <div class="error-image">
          <ImageView
            src="https://www.youbaobao.xyz/resource/icon/crash.png"
          />
        </div>
        <div class="error-msg">{{error.message || '程序猿紧急抢修中...'}}</div>
        <div class="error-retry-wrapper">
          <div class="error-retry" @click="retry">重启小程序</div>
        </div>
      </div>
    </div>
    <slot v-if="!error"></slot>
  </div>
</template>

<script>
  import store from '../store'
  import { setError } from '../utils/error'
  import ImageView from './base/ImageView'

  export default {
    components: { ImageView },
    computed: {
      error() {
        return store.state.error
      }
    },
    methods: {
      retry() {
        // 跳转回到首页
        let path = getApp().globalData.appOptions.path
        if (!path.startsWith('/')) {
          path = `/${path}`
        }
        mpvue.reLaunch({ url: path })
        // 重置异常信息
        setError()
      }
    }
  }
</script>

<style lang="scss" scoped>
  
</style>
