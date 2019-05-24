<template>
	<div class="wrapper">
		<TheIntro />
		<div v-if="response">
			<!-- <pre>{{ response }}</pre> -->
			<div class="card-wrap">
				<WeatherCard
					v-for="(dailyForecast, index) in filteredResponse"
					v-bind="dailyForecast"
					:city=response.city
					:key="index"
				/>
			</div>
		</div>
		<div v-else>
			<h3>Eek! Something Went Wrong...</h3>
			<div v-html="responseError"></div>
		</div>
	</div>
</template>

<script>
	import TheIntro from './components/TheIntro.vue';
	import WeatherCard from './components/WeatherCard.vue';
	const axios = require('axios');

	export default {
		components: {
			TheIntro,
			WeatherCard
		},

		computed: {
			// API returns 40 total times across 5 days; we are only interested in one time per day, so return each 8th time
			filteredResponse() {
				return this.response.list.filter((v, i) => i % 8 === 0);
			}
		},
		
		created () {
			this.loadWeatherData();
		},
		
		data() {
			return {
				apiKey: 'b2763e469c8ae7d0017e29614b8b9cd7',
				response: null,
				responseError: null
			}
		},
		
		methods: {
			loadWeatherData() {
				let self = this;
				axios
					// .get('https://api.openweathermap.org/data/2.5/forecast?id=6542285&units=imperial&APPID=' + self.apiKey)
					.get('http://localhost:8080/weather-data.json')
					.then(function(response) {
						self.response = response.data;
					})
					.catch(function(error) {
						self.responseError = error
					});
			}
		},
	};
</script>

<style lang="scss">
	@import "scss/base.scss";

	// TODO: move these to scoped component files
	.wrapper {
		margin: 0 auto;
		max-width: $wrapper-width;
	}

	.card-wrap {
		display: flex;
		justify-content: space-between;
	}
</style>
