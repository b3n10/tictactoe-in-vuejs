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
	margin: 0 auto;

	&__message {
		text-align: center;
	}
}
</style>
