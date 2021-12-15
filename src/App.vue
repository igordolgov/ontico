<template>
	<div id="app">
		<MainPage />
	</div>
</template>

<script>
	import MainPage from '@/components/MainPage.vue'

	export default {
		name: 'App',
		components: { MainPage }
	}
</script>

<style>
	#app {
		margin-top: 60px;
	}
</style>
