<template>
<div class="icons">
    <swiper :options="swiperOption">
        <swiper-slide v-for="(page, index) of pages" :key="index" >
            <!-- 循环的数组不再是iconList而是pages -->
            <div class="icon" v-for="item of page" :key="item.id" >
                <div class="icon-img">
                    <img class="icon-img-content" :src="item.imgUrl">
                </div>
                <p class="icon-desc">{{item.desc}}</p>
            </div>
        </swiper-slide>
        <!-- <swiper-slide>
            <div class="icon">
                <div class="icon-img">
                    <img class="icon-img-content" src="http://img1.qunarzz.com/piao/fusion/1804/5a/13ceb38dcf262f02.png">
                </div>
                <p class="icon-desc">一日游</p>
            </div>
        </swiper-slide> -->
    </swiper>
</div>

</template>

<script>
export default{
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        autoplay: false
      }
    }
  },
  computed: {
    pages () {
      const pages = []
      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
@import '~styles/mixins.styl'
.icons >>> .swiper-container
    height:0
    padding-bottom:50%
.icons
    width:100%
    height:0
    padding:5% 0 55%
    overflow:hidden

    .icon
        position:relative
        float:left;
        width:25%
        height:0
        padding-bottom:25%

        .icon-img
            position:absolute
            top:0
            left:0
            right:0
            bottom:.44rem

            box-sizing:border-box
            .icon-img-content
                display:block
                margin:0 auto
                height:100%
        .icon-desc
            position:absolute
            left:0
            right:0
            bottom:0
            line-height: .44rem
            color:$darkTextColor
            text-align:center
            ellipsis()
</style>
