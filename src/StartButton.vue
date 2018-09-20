<template>
	<div class="btn">
		<div class="btn__x" @click="$emit('start', false)">
			X
		</div>
		<div class="btn__o" @click="$emit('start', true)">
			O
		</div>
	</div>
</template>

<script>
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Ubuntu:700');

.btn {
	margin: 0 auto;
	display: flex;
	width: 300px;
	justify-content: space-around;

	&__x, &__o {
		display: inline-block;
		font-family: 'Ubuntu', sans-serif;
		font-size: 3rem;
		font-weight: 900;
		line-height: 1.25;
		background: #555;
		color: #f1f1f1;
		height: 60px;
		width: 60px;
		text-align: center;
		border-radius: 5px;
		cursor: pointer;
	}
}
</style>
