<template>
  <div class="wrapper">
    <div class="list" ref="list">
      <div>
        <div class="city-area">
          <h1 class="city-title">当前城市</h1>
          <ul class="city-list">
            <li class="city-wrapper">
              <div class="city">{{this.currentCity}}</div>
            </li>
          </ul>
        </div>
        <div class="city-area">
          <h1 class="city-title">热门城市</h1>
          <ul class="city-list">
            <li
              class="city-wrapper"
              v-for="item in hotCities"
              :key="item.id"
              @click="handleChangeCity(item.name)"
            >
              <div class="city">{{item.name}}</div>
            </li>
          </ul>
        </div>
        <div class="city-area" v-for="(item, key) in cities" :key="key" :ref="key">
          <h1 class="city-title">{{key}}</h1>
          <ul class="item-list">
            <li
              class="item border-bottom"
              v-for="innerItem in item"
              :key="innerItem.id"
              @click="handleChangeCity(innerItem.name)"
            >
              {{innerItem.name}}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import BScroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'

export default {
  name: 'CityList',
  props: {
    cities: {
      type: Object
    },
    hotCities: {
      type: Array
    },
    letter: {
      type: String
    }
  },
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  methods: {
    handleChangeCity(city) {
      // this.$store.dispatch('changeCity', city)
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations({
      changeCity: 'changeCity'
    })
  },
  mounted() {
    this.scroll = new BScroll(this.$refs.list)
  },
  watch: {
    letter() {
      const element = this.$refs[this.letter][0]
      this.scroll.scrollToElement(element)
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
  @import '~styles/variables.styl'
  .border-bottom
    &:before
      border-color: #ccc
  .list
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    overflow: hidden
    .city-title
      display: block
      height: .74rem
      line-height: .74rem
      text-indent: .2rem
      font-size: .24rem
      background: #f5f5f5
      color: $textColor
    .city-list
      overflow: hidden
      padding: .1rem .6rem .1rem .1rem
      .city-wrapper
        width: 33.33%
        float: left
      .city
        margin: .1rem
        padding: .1rem 0
        text-align: center
        border: .02rem solid #ccc
        border-radius: .06rem
        color: $textColor
    .item-list
      line-height: .9rem
      text-indent: .2rem
      font-size: .28rem
      color: $textColor
</style>
