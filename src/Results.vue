<template>
	<div class="results">
		<div class="results__message">
			{{ rlt }}
		</div>
	</div>
</template>

<script>
export default {
	props: ['rlt']
}
</script>

<style lang="scss">
.results {
	margin: 0;
	position: fixed;
	left: 0;
	right: 0;
	top: 3%;

	&__message {
		text-align: center;
	}
}
</style>
