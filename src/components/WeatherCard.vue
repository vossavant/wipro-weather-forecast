<template>
	<article class="weather-card" :class="formattedType">
		<div class="weather-card__inner">
			<div class="weather-conditions">
				<span class="weather-type">{{ weather[0].main }}</span>
				<span class="weather-temp">{{ formattedTemp }}&deg;</span>
			</div>
			<div class="weather-meta">
				<header>
					<span class="weather-day">{{ formattedDay }}</span>
					<h1>{{ formattedMonth }} {{ formattedDate }}</h1>
				</header>
                <dl>
                    <div title="Cloud Cover">
                        <dt class="clouds">Cloud Cover</dt>
                        <dd>{{ clouds.all }}%</dd>
                    </div>
                    <div title="Wind speed and direction">
                        <dt class="wind">Wind</dt>
                        <dd>{{ wind.speed }} mph / {{ wind.deg }}</dd>
                    </div>
                    <div title="Humidity">
                        <dt class="humidity">Humidity</dt>
                        <dd>{{ main.humidity }}%</dd>
                    </div>
                </dl>
			</div>
		</div>
	</article>
</template>

<script>
	export default {
		computed: {
			formattedDate() {
				return this.dateTime.getDate();
			},

			formattedDay() {
				return new Date().getDay() === this.dateTime.getUTCDay()
					? "Today"
					: this.dateTime.toLocaleString("default", { weekday: "short" });
			},

			formattedMonth() {
				return this.dateTime.toLocaleString("default", { month: "long" });
			},

			formattedTemp() {
				return Math.round(this.main.temp);
			},

			formattedType() {
				return "weather-card--" + this.weather[0].main.toLowerCase();
			}
		},

		data() {
			return {
				dateTime: new Date(this.dt * 1000)
			};
		},

		props: {
			clouds: Object,
			dt: {
                type: Number,
                required: true
			},
			main: {
                type: Object,
                required: true
			},
			weather: {
                type: Array,
                required: true
            },
            wind: Object
		}
	};
</script>

<style lang="scss" scoped>
    dl,
    dd {
        margin: 0;
    }

    dl {
        display: flex;
    }

    dd {
        width: 33%;
    }

    dt {
        background-repeat: no-repeat !important;
        background-position: center left !important;
        line-height: 24px;
        overflow: hidden;
        text-indent: 100%;
        white-space: nowrap;

        &.clouds {
            background: url('../assets/cloud.svg');
        }
    
        &.humidity {
            background: url('../assets/droplet.svg');
        }
    
        &.wind {
            background: url('../assets/wind.svg');
        }
    }

	h1 {
        font-size: 24px;
		margin-top: 8px;
	}

	header {
		position: relative;
	}

	.weather-card {
		background-position: top center !important;
		border-radius: 8px;
		box-shadow: 2px 2px 8px transparentize(black, 0.9);
		overflow: hidden;
		position: relative;
		width: 19%;

		&:before {
			background: -moz-linear-gradient(
				top,
				rgba(0, 0, 0, 0.65) 0%,
				rgba(0, 0, 0, 0) 100%
			);
			background: -webkit-linear-gradient(
				top,
				rgba(0, 0, 0, 0.65) 0%,
				rgba(0, 0, 0, 0) 100%
			);
			background: linear-gradient(
				to bottom,
				rgba(0, 0, 0, 0.65) 0%,
				rgba(0, 0, 0, 0) 100%
			);
			filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#a6000000', endColorstr='#00000000',GradientType=0 );
			bottom: 0;
			content: "";
			position: absolute;
			top: 0;
			left: 0;
			right: 0;
		}

		&--clouds {
			// Unsplash: https://unsplash.com/photos/4C6Rp23RjnE
			background: url("../assets/weather/clouds.jpg");
		}

		&--rain {
			// Unsplash: https://unsplash.com/photos/1YHXFeOYpN0
			background: url("../assets/weather/rain.jpg");
		}

		&__inner {
			position: relative;
		}
	}

	.weather-conditions {
		color: white;
		height: 288px;
        padding: 24px;
        text-shadow: 1px 1px 4px transparentize(black, 0.65);
	}

	.weather-day {
		font-size: 12px;
		letter-spacing: 2px;
		opacity: 0.35;
		text-transform: uppercase;
	}

	.weather-meta {
		background: white;
		padding: 24px;
		position: relative;

		&:after,
		&:before {
			background: white;
			content: "";
			height: 32px;
			left: -4px;
			position: absolute;
			right: -4px;
			top: -16px;
			transform: rotate(-6deg);
		}

		&:after {
            background: transparentize($color: white, $amount: 0.5);
			border-top-right-radius: 2px;
			right: 24px;
			top: -24px;
		}
	}

	.weather-temp {
		display: block;
		font-size: 48px;
	}

	.weather-type {
		display: block;
        font-size: 18px;
		margin-bottom: 6px;
        opacity: 0.7;
	}
</style>
