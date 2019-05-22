<template>
	<h2>{{ title }}</h2>
</template>


<script>
	export default {
		name: 'notes-header',
		props: {
			title: {
				type: String,
				default: 'Notes App',
			},
		},
	};
</script>


<style lang="scss" scoped>
	h2 {
		padding-top: 10px;
		text-align: center;
		font-weight: 500;
		color: #44c767;
		text-shadow: 0 2px 3px rgba(255, 255, 255, 0.5);
	}
</style>
