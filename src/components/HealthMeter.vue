<template>
	<div class="progress-bar">
		<div v-bind:style="{width : meterWidth + '%'}" class="progress-amount" ></div>
	</div>	
</template>

<script>
	export default {
		props: ['meter-width'],
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style lang="scss">
	.progress-bar {
	background: #eee;
	border: 1px solid #aaa;
	height: 15px;
	.progress-amount {
		background: green;
		height: 100%;
		transition: .5s ease all;
	}
}
</style>