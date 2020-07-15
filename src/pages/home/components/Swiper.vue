<template>
  <div class="wrapper">
    <swiper :options="swiperOptions" v-if="showSwiper">
      <swiper-slide v-for="item of list" :key="item.id">
        <img class="swiper-img" :src="item.imgUrl"/>
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: "HomeSwpier",
  props: {
    list:Array
  },
  data() {
    return {
      swiperOptions: {
        pagination: {
          el: ".swiper-pagination",
        },
        loop: true,
        autoplay: 1000,
        // Some Swiper option/callback...
      },
      // list:[{
      //   imgUrl: 'https://img-blog.csdnimg.cn/20200208181017569.gif'
      // },{
      //   imgUrl: 'https://img-blog.csdnimg.cn/20200208181013160.gif'
      // },{
      //   imgUrl:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594826521464&di=ad9cefe720f312970f918e8f2b4e49a0&imgtype=0&src=http%3A%2F%2Fa.hiphotos.baidu.com%2Fzhidao%2Fpic%2Fitem%2Fd50735fae6cd7b89a6c4a5d60d2442a7d9330e3e.jpg'
      // }]
    };
  },
    computed: {
      showSwiper () {
      return this.list.length
      }
      },
};
</script>

<style lang="stylus" scoped>
  .wrapper >>> .swiper-pagination-bullet-active
    background: #fff
  .wrapper
    overflow: hidden
    width: 100%
    height: 0
    padding-bottom: 31.25%
    background: #eee
    .swiper-img
      width: 100%
</style>
