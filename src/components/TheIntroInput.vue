<template>
	<span>
		<input type="text" placeholder="any city in the world" :value="location" @input="lookupWeather">
		You entered: {{ location }}
	</span>
</template>

<script>
	const _ = require("lodash");
    const axios = require('axios');

	export default {
		data() {
			return {
                apiKey: 'b2763e469c8ae7d0017e29614b8b9cd7',
				forecastData: null,
				forecastDataError: null,
				location: ""
			};
        },
        
		methods: {
			lookupWeather: _.debounce(function(e) {
                let self = this;
                this.location = e.target.value;

                axios
					.get('https://api.openweathermap.org/data/2.5/forecast?q=' + e.target.value + '&units=imperial&APPID=' + self.apiKey)
					// .get('https://api.openweathermap.org/data/2.5/forecast?id=6542285&units=imperial&APPID=' + self.apiKey)
					// .get('http://localhost:8080/weather-data.json')
					.then(function(forecastData) {
						self.forecastData = forecastData.data;
						self.$emit('forecast', forecastData.data);
					})
					.catch(function(error) {
						self.forecastDataError = error;
						self.$emit('forecastError', error);
					});
			}, 500)
		}
	};
</script>

<style lang="scss" scoped>
	input {
		border: 0;
		border-bottom: 2px solid #ccc;
		font-size: 48px;
	}
</style>