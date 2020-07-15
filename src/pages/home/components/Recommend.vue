<template>
  <div>
    <div class="title">热销推荐</div>
    <ul>
      <li v-for="item of list" :key="item.id" class="item border-bottom">
       <img class="item-img" :src="item.imgUrl" />
        <div class="item-info">
          <p class="item-title">{{item.title}}</p>
          <p class="item-desc">{{item.desc}}</p>
          <button class="item-button">查看详情</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HomeRecommend",
  props: {
    list:Array
  },
  data: function(){
    return {
      // list: [
      //   {
      //     id:'001',
      //     title:'AAAhahahhahhahahahahhahahahahahh',
      //     desc:'哈哈哈哈啊哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或',
      //     imgUrl:'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1995235764,179833910&fm=26&gp=0.jpg'
      //   },
      //   {
      //     id:'002',
      //     title:'AAAhahahhahhahahahahhahahahahahh',
      //     desc:'哈哈哈哈啊哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或',
      //     imgUrl:'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg'
      //   },
      //   {
      //     id:'003',
      //     title:'AAAhahahhahhahahahahhahahahahahh',
      //     desc:'哈哈哈哈啊哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或',
      //     imgUrl:'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1995235764,179833910&fm=26&gp=0.jpg'
      //   },
      //   {
      //     id:'004',
      //     title:'AAAhahahhahhahahahahhahahahahahh',
      //     desc:'哈哈哈哈啊哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或',
      //     imgUrl:'http://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_50x50.jpg'
      //   },
      //   {
      //     id:'005',
      //     title:'AAAhahahhahhahahahahhahahahahahh',
      //     desc:'哈哈哈哈啊哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或或',
      //     imgUrl:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594826520535&di=df6c4190346b318050a09885c5bd7874&imgtype=0&src=http%3A%2F%2Fbos.pgzs.com%2Frbpiczy%2FWallpaper%2F2013%2F10%2F8%2F02404ff49fee4263ba88311605c47608.jpg'
      //   },
      // ]
    }
  }
};
</script>
<style lang="stylus" scoped>
  @import '~styles/mixins.styl'
  .title
    margin-top: .2rem
    line-height: .8rem
    background: #eee
    text-indent: .2rem
  .item
    overflow: hidden
    display: flex
    height: 1.9rem
    .item-img
      width: 1.7rem
      height: 1.7rem
      padding: .1rem
    .item-info
      flex: 1
      padding: .1rem
      min-width: 0
      .item-title
        line-height: .54rem
        font-size: .32rem
        ellipsis()
      .item-desc
        line-height: .4rem
        color: #ccc
        ellipsis()
      .item-button
        line-height: .44rem
        margin-top: .16rem
        background: #ff9300
        padding: 0 .2rem
        border-radius: .06rem
        color: #fff
</style>
