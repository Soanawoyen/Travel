<template>
	<div class="wrapper">
		<swiper :options="swiperOption">
		<!-- slides -->
		<swiper-slide v-for="item of swiperList"
			:key="item.id">
			<img :src="item.imgUrl" class="swiper-img">
		</swiper-slide>
		<!-- Optional controls -->
		<div class="swiper-pagination"  slot="pagination"></div>
		</swiper>
	</div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  props: {
	  swiperList: Array
  },	
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
	  	}
	  }
    }
  }
</script>

<style scoped>
	.wrapper{
		overflow: hidden;
		width: 100%;
		height: 0;
		padding-bottom: 35%;
	}
	.swiper-img{
		width: 100%;
	}
</style>
