<template>
	<div class="btn">
		<button class="btn__x" @click="$emit('start', false)">Play as X</button>
		<button class="btn__O" @click="$emit('start', true)">Play as O</button>
	</div>
</template>

<script>
</script>

<style lang="scss">
.btn {
	margin: 50px auto;
	width: 166px;
}
</style>
