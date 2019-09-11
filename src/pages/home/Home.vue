<template>
  <div>
        <home-header></home-header>
		<home-swiper :swiperList="swiperList"></home-swiper>
		<home-icons :list="list"></home-icons>
		<home-recommend :recommendList="recommendList"></home-recommend>
		<home-weeken :weekendList="weekendList"></home-weeken>
  </div>
</template>

<script>
import HomeHeader from './components/Header'
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeWeeken from './components/Weeken'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    HomeHeader,
    HomeSwiper,
	HomeIcons,
	HomeRecommend,
	HomeWeeken
  },
  data () {
	  return {
		  swiperList: [],
		  list:[],
		  recommendList: [],
		  weekendList: []
	  }
  },
  methods: {
    getHomeInfo () {
      axios.get('/api/index.json')
        .then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc (res) {
      res = res.data
      if (res.ret && res.data) {
		const data = res.data
        this.swiperList = data.swiperList
        this.list = data.iconList
        this.recommendList = data.recommendList
		this.weekendList = data.weekendList
		console.log(this.city,this.swiperList,this.list,this.recommendList,this.weekendList)
      }
    }
  },
  mounted() {
	  this.getHomeInfo()
  }
}
</script>

<style>

</style>
