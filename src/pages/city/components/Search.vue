<template>
	<div>
		<div class="search">
			<input v-model="keyWord" type="text" placeholder="输入城市名或拼音" class="search-input">
		</div>
		<div class="search-content" ref="search" 
			v-show="keyWord"
		>
			<ul>
				<li class="search-item border-bottom"
				v-for="item of list" :key="item.id"
				@click="handleCityClick(item.name)"
				>
					{{item.name}}
				</li>
				<li v-show="list.length" 
				class="search-item border-bottom">
					没有找到匹配数据
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
import Bscroll from 'better-scroll'

export default {
	name: 'CitySearch',
	props:{
		cities: Object
	},
	data () {
		return {
			keyWord: '',
			list: [],
			timer: null
		}
	},
	methods: {
		handleCityClick (city) {
			this.$store.commit('changeCity', city)
			// alert(city)
			// 点击后跳转
			this.$router.push('/')
		}
	},
	watch :{
		keyWord () {
			if(this.timer) {
				clearTimeout(this.timer)
			}
			if(!this.keyWord) {
				this.list = []
				return 
			}
			this.timer = setTimeout(() => {
				const result = []
				for(let i in this.cities) {
					this.cities[i].forEach((value) => {
						if(value.spell.indexOf(this.keyWord) > -1 || value.name.indexOf(this.keyWord) > -1) {
							result.push(value)
						}
					})
				}
				this.list = result
			}, 100)
		}
	},
	mounted () {
		this.scroll = new Bscroll(this.$refs.search)
	}
}
</script>

<style lang="stylus"scoped>
  @import '~@/assets/styles/varibles.styl'
  .search
    height: .72rem
    padding: 0 .1rem
    background: $bgColor
    .search-input
      box-sizing: border-box
      width: 100%
      height: .62rem
      padding: 0 .1rem
      line-height: .62rem
      text-align: center
      border-radius: .06rem
      color: #666
  .search-content
    z-index: 1
    overflow: hidden
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    background: #eee
    .search-item
      line-height: .62rem
      padding-left: .2rem
      background: #fff
      color: #666
</style>
