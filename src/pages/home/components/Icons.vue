<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide v-for="(page, index) of pages" :key="index">
        <div
          class="icon"
          v-for="item of page"
          :key="item.id"
        >
          <div class='icon-img'>
            <img class='icon-img-content' :src='item.imgUrl' />
          </div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data () {
  return {
    swiperOption: {
      autoplay: false
      },
      // list:[
      //   {
      //     id:'001',
      //     imgUrl: 'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg',
      //     desc: '淘宝哈哈哈我最帅'
      //   },
      //    {
      //     id:'002',
      //     imgUrl: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1995235764,179833910&fm=26&gp=0.jpg',
      //     desc: '淘宝'
      //   },
      //    {
      //     id:'003',
      //     imgUrl: 'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg',
      //     desc: '淘宝'
      //   },
      //    {
      //     id:'004',
      //     imgUrl: 'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg',
      //     desc: '淘宝'
      //   },
      //     {
      //     id:'005',
      //     imgUrl: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1995235764,179833910&fm=26&gp=0.jpg',
      //     desc: '淘宝'
      //   },
      //     {
      //     id:'006',
      //     imgUrl: 'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg',
      //     desc: '淘宝'
      //   },
      //     {
      //     id:'007',
      //     imgUrl: 'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg',
      //     desc: '淘宝'
      //   },
      //     {
      //     id:'008',
      //     imgUrl: 'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg',
      //     desc: '淘宝'
      //   },
      //     {
      //     id:'009',
      //     imgUrl: 'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg',
      //     desc: '淘宝'
      //   },
      //     {
      //     id:'010',
      //     imgUrl: 'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg',
      //     desc: '淘宝'
      //   },
      // ]
    }
  },
  computed: {
    pages(){
      const pages = []
      this.list.forEach((item, index) => {
        const page = Math.floor(index/8)
        if(!pages[page]){
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  },
}
</script>

<style lang="stylus" scoped>
 @import '~styles/varibles.styl'
  @import '~styles/mixins.styl'
  .icons >>> .swiper-container
    height: 0
    padding-bottom: 50%
  .icons
    margin-top: .1rem
    .icon
      position: relative
      overflow: hidden
      float: left
      width: 25%
      height: 0
      padding-bottom: 25%
      .icon-img
        position: absolute
        top: 0
        left: 0
        right: 0
        bottom: .44rem
        box-sizing: border-box
        padding: .1rem
        .icon-img-content
          display: block
          margin: 0 auto
          height: 100%
      .icon-desc
        position: absolute
        left: 0
        right: 0
        bottom: 0
        height: .44rem
        line-height: .44rem
        text-align: center
        color: $darkTextColor
        ellipsis()
</style>
