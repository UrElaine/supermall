<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <home-swiper :banners="banners"/>
    <recommend-view :recommends="recommends"/>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'
import HomeSwiper from "./childComps/HomeSwiper"
import RecommendView from './childComps/RecommendView'


import {getHomeMutiData} from 'network/home'

export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView
  },
  data(){
    return {
      banners: [],
      recommends: []
    }
  },
  //生命周期函数
  created() {
    //1.请求数据
    getHomeMutiData().then(res => {
      //res是局部变量，函数执行完之后就会从内存中回收
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    })
  }

}
</script>

<style scoped>
.home-nav {
  background-color: var(--color-tint);
}
</style>
