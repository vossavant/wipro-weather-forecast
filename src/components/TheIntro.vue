<!--
	The Intro

	Master heading and intro paragraph for the entire app.
-->
<template>
	<header>
		<TheLogo />
		<h1>Weather Forecast</h1>
		<p
			class="intro-p"
		>Some language about the app goes here...</p>
	</header>
</template>

<script>
    import TheLogo from './TheLogo.vue';

	export default {
        components: {
            TheLogo,
        }
    };
</script>

<style lang="scss" scoped>
	
</style>