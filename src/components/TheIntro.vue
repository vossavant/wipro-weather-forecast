<!--
	The Intro

	Master heading and intro paragraph for the entire app.
-->
<template>
	<header>
		<TheLogo />
		<h1>Going Somewhere?</h1>
		<div>
			<p>Get the current and five-day forecast for <TheIntroInput @forecast="something" /> so you can, as the Boy Scouts say, <strong>be prepared.</strong></p>
		</div>
		Here's the forecast: {{ something }}
	</header>
</template>

<script>
	import TheLogo from './TheLogo.vue';
	import TheIntroInput from './TheIntroInput.vue';

	export default {
		data() {
			return {
				something: null
			}
		},
        components: {
			TheLogo,
			TheIntroInput
        }
    };
</script>

<style lang="scss" scoped>
	h1 {
		font-size: 48px;
		margin-bottom: 0;
	}

	header {
		margin-bottom: 48px;
	}

	p {
		font-size: 48px;
    	line-height: 1.2;
		margin-top: 24px;
	}
</style>