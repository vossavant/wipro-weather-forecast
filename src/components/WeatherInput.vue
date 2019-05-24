<template>
	<span>
		<input type="text" placeholder="any city in the world" :value="location" @input="lookupWeather">
		You entered: {{ location }}
	</span>
</template>

<script>
	var _ = require("lodash");

	export default {
		data() {
			return {
				location: ""
			};
        },
        
		methods: {
			lookupWeather: _.debounce(function(e) {
				this.location = e.target.value;
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