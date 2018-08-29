<template>
  <div>
    <div class="item" v-for="(item, index) of list" :key="index">
      <div class="item-title">
        <span class="item-title-icon"></span>
        {{item.title}}
      </div>
      <div v-if="item.children" class="item-children">
        <detail-list :list="item.children"></detail-list>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'DetailList',
  props: {
    list: Array
  }
}
</script>
<style lang="stylus" scoped>
.item-title
  line-height: .8rem
  font-size: .32rem
  padding: 0 .2rem 0 .6rem
  border-bottom: 1px solid #eee
  position:relative
  .item-title-icon
    display: inline-block
    position: absolute
    width: .36rem
    height: .36rem
    top: .2rem
    left: .2rem
    background: url(http://s.qunarzz.com/piao/image/touch/sight/detail.png) 0 -.44rem no-repeat
    margin-right: .1rem
    background-size: .4rem 3rem
.item-children
  padding:0 .2rem
  color: #666
  font-size:.24rem
</style>
