<template>
	<div>
		<city-header></city-header>
		<city-search :cities="cities"></city-search>
		<city-list :hot="hotCities" 
			:cities="cities"
			:letter="letter"
		></city-list>
		<city-ahplabet :cities="cities"
			@change="handleLetterChange"
		></city-ahplabet>
	</div>
</template>

<script>
import axios from 'axios'
import CityHeader from './components/CityHeader'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAhplabet from './components/Ahplabet'
export default {
	name: 'City',
	components: {
		CityHeader,
		CitySearch,
		CityList,
		CityAhplabet
	},
	data () {
		return {
			cities: {},
			hotCities: [],
			letter:''
		}
	},
	methods: {
		getCityInfo () {
			axios.get('/api/city.json')
				.then(this.handleGetCityInfoSucc)
		},
		handleGetCityInfoSucc (res) {
			res = res.data;
			if (res.ret && res.data) {
				const data = res.data
				this.cities = data.cities
				this.hotCities = data.hotCities
			}
		},
		handleLetterChange (letter) {
			this.letter = letter
		} 
	},
	mounted () {
		this.getCityInfo()
	}
}
</script>

<style lang="stylus"scoped>

</style>
