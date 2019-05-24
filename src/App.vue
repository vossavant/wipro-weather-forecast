<template>
	<div class="wrapper">
		<!-- <TheIntro /> -->
		<TheIntroInput @forecast="forecastData = $event" @forecastError="forecastDataError = $event" />
		<div v-if="forecastData">
			<!-- <pre>{{ response }}</pre> -->
			<div class="card-wrap">
				<WeatherCard
					v-for="(dailyForecast, index) in filteredForecastData"
					v-bind="dailyForecast"
					:city=forecastData.city
					:key="index"
				/>
			</div>
		</div>
		<div v-else-if="forecastDataError">
			<h3>Eek! Something Went Wrong...</h3>
			<div v-html="forecastDataError"></div>
		</div>
		<div v-else>
			<h3>Waiting for you to enter something...</h3>
		</div>
	</div>
</template>

<script>
	// import TheIntro from './components/TheIntro.vue';
	import TheIntroInput from './components/TheIntroInput.vue';
	import WeatherCard from './components/WeatherCard.vue';

	export default {
		components: {
			// TheIntro,
			TheIntroInput,
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
