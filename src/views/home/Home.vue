<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <home-swiper :banners="banners"></home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control class="tab-control" :titles="['流行', '新款', '精选']" @tabclick="tabClick"></tab-control>
    <!-- <goods-list :goods="showGoods"></goods-list> -->
    <div>
      <h2>请求接口无数据</h2>
      <h2>请求接口无数据</h2>
      <h2>请求接口无数据</h2>
      <h2>请求接口无数据</h2>
      <h2>请求接口无数据</h2>
      <h2>请求接口无数据</h2>
      <h2>请求接口无数据</h2>
      <h2>请求接口无数据</h2>
    </div>
  </div>
</template>

<script>
import { getHomeMultidata, getHomeGoods } from '../../network/home'



import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/HomeRecommendView'
import FeatureView from './childComps/FeatureView'

import NavBar from '../../components/common/navbar/NavBar'
import TabControl from '../../components/content/tabControl/TabControl'
// import GoodsList from '../../components/content/goods/GoodsList'



export default ({
  name: 'Home',
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop': {page: 0, list: []},
        'news': {page: 0, list: []},
        'sell': {page: 0, list: []}
      },
      currentType: 'pop'
    }
  },
  // computed: {
  //   showGoods() {
  //     return this.goods[this,currentType].list
  //   }
  // },
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    // GoodsList
  },
  created() {
    // 请求多个数据
    this.getHomeMultidata()

    // 请求商品数据
    // this.getHomeGoods()

  },
  methods: {
    // 事件监听
    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = 'pop'
          break
        case 1:
          this.currentType = 'news'
          break
        case 2:
          this.currentType = 'sell'
          break
      }
    },

    // 网络请求
    getHomeMultidata() {
      getHomeMultidata().then(res => {
      // console.log(res)
      this.banners = res.data.banner.list
      this.recommends = res.data.recommend.list
    })
    },
    // getHomeGoods(type) {
    //   const page = this.goods[type].page + 1
    //   getHomeGoods(type, page).then(res => {
    //     this.goods[type].list.push(...res.data.list)
    //     this.goods[type].page += 1
    //   })
    // }
  }
})
</script>

<style scoped>
  #home {
    padding-top: 44px;
  }
  .home-nav {
    background-color: var(--color-tint);
    color: #fff;
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    background-color: #fff;
    z-index: 10000000;
  }
  .tab-control {
    position: sticky;
    top: 44px;
    z-index: 9;
  }
</style>
