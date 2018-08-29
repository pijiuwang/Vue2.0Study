<template>
    <div class="header">
       <div class="header-left">
            <div class="iconfont back-icon">&#xe62d;</div>
       </div>
       <div class="header-input"><span class="iconfont ">&#xe632;</span>输入城市/景点/游玩主题</div>
       <router-link to='/city'>
          <div class="header-right">{{this.city}}<span class="iconfont arrow-icon">&#xe62d;</span></div>
       </router-link>
    </div>
</template>
<script>
import { mapState } from 'vuex'
export default{
  name: 'HomeHeader',
  computed: {
    ...mapState(['city']) // 把city这个公用数据映射到名字叫city的计算属性中
  }
}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl'
/*1rem = html font-size=50px*/
 .header
  height: $headerHeight
  display:flex
  line-height: $headerHeight
  color:#fff
  background:$bgColor
  .header-left
    width:.64rem
    .back-icon
      text-align:center
      font-size:.4rem
  .header-input
    flex:1
    height:.62rem
    line-height:.62rem
    margin-top:.12rem
    margin-left:.2rem
    border-radius:.1rem
    background:#fff
    color:#ccc
    text-indent:.2rem
  .header-right
    min-width:1.04rem
    padding:0 .1rem
    float:right
    text-align:center
    color:#fff
    .arrow-icon
        font-size:.24rem
        margin-left:.1rem
  .box
    height:0
    width:100%;

</style>
