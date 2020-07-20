<template>
  <div>
    <detail-banner
      :sightName="sighName"
      :bannerImg="bannerImg"
      :bannerImgs="gallaryImgs"
      ></detail-banner>
    <detail-header></detail-header>
    <detail-list :list="list"></detail-list>
    <div class="sty"></div>
  </div>
</template>

<script>
import DetailBanner from './components/Banner'
import DetailHeader from './components/Header'
import DetailList from './components/list'
import axios from 'axios'
export default {
  name:'Detail',
  components:{
    DetailBanner,
    DetailHeader,
    DetailList
  },
  data() {
    return {
      sighName: '',
      bannerImg: '',
      gallaryImgs: [],
      list:[]
    }
  },
  methods: {
    getDetailInfo(){
      axios.get('/api/detail.json',{
        params: {
          id: this.$route.params.id
        }
      }).then(this.handleGetDataSucc)
    },
    handleGetDataSucc(res){
      // console.log(res)
      res = res.data
      if(res.ret && res.data){
        const data = res.data
        this.sighName = data.sighName
        this.bannerImg = data.bannerImg
        this.gallaryImgs = data.gallaryImgs
        this.list = data.categoryList
      }
    }
  },
  mounted() {
    this.getDetailInfo()
  },
}
</script>

<style lang="stylus" scoped>
  .sty
    height: 50rem;
</style>
