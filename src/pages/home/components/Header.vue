<template>
  <div class="header">
    <div class="header-left">
      <div class="iconfont back-icon">&#xe624;</div>
    </div>
    <div class="header-center">
      <span class="iconfont search-icon">&#xe632;</span>
      输入城市/景点/游玩主题
    </div>
    <router-link to="/city">
      <div class="header-right">
        {{this.currentCity}}<span class="iconfont arrow-icon">&#xe64a;</span>
      </div>
    </router-link>
  </div>
</template>

<script type="text/ecmascript-6">
import { mapState } from 'vuex'

export default {
  name: 'HomeHeader',
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
  @import '~styles/variables.styl'
  .header
    display: flex
    height: .86rem
    line-height: .86rem
    background: $bgColor
    color: #fff
    .header-left
      width: .64rem
      float: left
      .back-icon
        text-align: center
        width: .8rem
        font-size: .4rem
        font-weight: bold
    .header-center
      flex: 1
      margin-top: .12rem
      margin-left: .2rem
      padding-left: .2rem
      height: .62rem
      line-height: .62rem
      background: #fff
      color: #ccc
      border-radius: .1rem
    .header-right
      min-width: 1.04rem
      padding: 0 .1rem
      float: right
      text-align: center
      color: #fff
      .arrow-icon
        font-size: .24rem
        margin-left: .04rem
</style>
