<template>
	<div class="wrapper">
		<TheLogo />
		<header class="intro">
			<h1>Going Somewhere?</h1>
			<p>Get the current and five-day forecast for <ApiRequestInput @forecast="forecastData = $event" @forecastError="forecastDataError = $event" /> so you can, as the Boy Scouts say, <strong>be prepared.</strong></p>
		</header>
		<div v-if="forecastDataError">
			<BaseNotification header="Sorry Charlie" content="Looks like that place only exists in your imagination. Try again!"/>
		</div>
		<div v-else-if="forecastData">
			<h2 class="forecast-header">5-Day Forecast for {{ forecastData.city.name }}, {{ forecastData.city.country }}</h2>
			<div class="card-wrap">
				<WeatherCard
					v-for="(dailyForecast, index) in filteredForecastData"
					v-bind="dailyForecast"
					:key="index"
				/>
			</div>
			<p class="credit">
				Weather data courtesy of <a href="https://openweathermap.org/">Open Weather Map</a>
			</p>
		</div>
		<div v-else>
			<BaseNotification header="Start Typing" content="Waiting for you to enter something..."/>
		</div>
	</div>
</template>

<script>
	import ApiRequestInput from './components/ApiRequestInput.vue';
	import BaseNotification from './components/BaseNotification.vue';
	import TheLogo from './components/TheLogo.vue';
	import WeatherCard from './components/WeatherCard.vue';

	export default {
		components: {
			BaseNotification,
			ApiRequestInput,
			TheLogo,
			WeatherCard
		},

		computed: {
			// API returns 40 total times across 5 days; we are only interested in one time per day, so return each 8th time
			filteredForecastData() {
				return this.forecastData.list.filter((v, i) => i % 8 === 0);
			}
		},

		data() {
			return {
				forecastData: null,
				forecastDataError: null
			}
		}
	};
</script>

<style lang="scss">
	@import "scss/base.scss";

	h2 {
		color: $secondary-text;
	}

	h2.forecast-header {
		border-top: 4px dotted #F9CFD7;
		color: $secondary-text;;
		padding-top: 1em;
		padding-bottom: 1em;
	}

	.intro {
		margin-bottom: 48px;
		
		h1 {
			background: $secondary-text;;
			border-radius: 8px;
			color: white;
			display: inline-block;
			font-size: 48px;
			margin-bottom: 0;
			margin-left: -8px;
			padding: 8px;
		}
	
		p {
			font-size: 48px;
			line-height: 1.2;
			margin-top: 24px;
		}
	}

	.credit {
		color: #b4b4b6;
		font-size: 12px;
		margin-top: 32px;
    	text-align: right;
	}

	// TODO: move these to scoped component files
	.wrapper {
		margin: 32px auto;
		max-width: $wrapper-width;
	}

	.card-wrap {
		display: flex;
		justify-content: space-between;
	}
</style>
