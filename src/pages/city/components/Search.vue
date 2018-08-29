<template>
  <div>
    <div class="search">
        <input class="search-input" type="text" placeholder="输入城市名或拼音" v-model="keyword" />
    </div>
    <div class="search-content" ref="search" v-show="keyword">
      <ul>
        <li v-for="item of list" class="search-item border-bottom" :key="item.id" @click="handleCityClick(item.name)">{{item.name}}</li>
        <li class="search-item border-bottom" v-show="hasNoData" >
            没有找到匹配数据
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import { mapMutations } from 'vuex'
// import { mapState, mapMutations } from 'vuex'
import Bscroll from 'better-scroll'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data() {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  computed: {
    hasNoData() {
      return !this.list.length
    }
  },
  watch: {
    keyword() {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      } // 如果keyword为空，让这个列表返回*清空状态
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach(value => {
            if (
              value.spell.indexOf(this.keyword) > -1 ||
              value.name.indexOf(this.keyword) > -1
            ) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  methods: {
    handleCityClick(city) {
      // this.$store.commit('changeCity', city)
      this.changeCity(city)
      this.$router.push('/') // 点击这个城市，然后页面跳转到首页
    },
    ...mapMutations(['changeCity'])
  },
  mounted() {
    this.scroll = new Bscroll(this.$refs.search)
  }
}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl'

.search
  position relative
  z-index 2
  display block
  height 0.62rem
  padding 0.1rem
  background $bgColor
  .search-input
    box-sizing border-box
    padding 0 0.1rem
    height 0.62rem
    line-height 0.62rem
    width 100%
    text-align center
    border-radius 0.06rem
    color #999
.search-content
  overflow hidden
  position absolute
  z-index 1
  top 1.58rem
  left 0
  right 0
  bottom 0
  background #eee
  .search-item
    line-height 0.62rem
    padding-left 0.2rem
    color #666
    background #fff
</style>
