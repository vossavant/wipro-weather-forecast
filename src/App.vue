<template>
	<div>
		<TheIntro />
		<div v-if="responseError">
			<h3>Eek! Something Went Wrong...</h3>
			<div v-html="responseError"></div>
		</div>
		<div v-else>
			<h3>Response</h3>
			{{ response }}
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
			loadWeatherData() {
				let self = this;
				axios
					// .get('https://api.openweathermap.org/data/2.5/forecast?id=524901&APPID=' + self.apiKey)
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
