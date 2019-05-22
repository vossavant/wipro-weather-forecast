<template>
	<div>
		<TheIntro />
		<div v-if="response">
			<h3>Response</h3>
			<h5>City: {{ response.city }}</h5>
			<pre>{{ response.list }}</pre>
			/////////
			<pre>{{ response }}</pre>
			=============================
			=============================
			=============================
			<div v-show="everyEighthResult(index)" v-for="(item, index) in response.list" :key="index">
				<h4>DT Text: {{ item.dt_txt }}</h4>
				<h4>Main: {{ item.main }}</h4>
				<pre>{{ item }}</pre>
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
	const axios = require('axios');

	export default {
		components: {
			TheIntro
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
			// API returns 40 total times across 5 days; we are only interested in one time per day, so return each 8th time
			everyEighthResult(i) {
				return i % 8 === 0;
			},

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

<style lang='scss'>
	h1 {
		color: saddlebrown;
	}
</style>
