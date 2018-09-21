<template>
	<div class="btn">
		<div v-if="shwBtn" class="btn__x" @click="$emit('start', false)">
			X
		</div>
		<div v-if="rlt" class="btn__result">
			{{ rlt }}
		</div>
		<div v-if="!rlt" class="btn__restart" @click="$emit('reset')">
			R E S T A R T
		</div>
		<div v-if="shwBtn" class="btn__o" @click="$emit('start', true)">
			O
		</div>
	</div>
</template>

<script>
export default {
	props: [ 'shwBtn', 'rlt' ]
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Ubuntu:700');

.btn {
	font-family: 'Ubuntu', sans-serif;
	margin: 0 auto;
	display: flex;
	width: 350px;
	justify-content: space-around;
	align-items: center;

	@media (min-width: 500px) {
		& {
			width: 500px;
		}
	}

	&__x,
	&__o {
		display: inline-block;
		font-size: 2.3rem;
		font-weight: 900;
		line-height: 40px;
		background: #555;
		color: #f1f1f1;
		height: 40px;
		width: 45px;
		text-align: center;
		border-radius: 5px;
		cursor: pointer;
	}

	&__result,
	&__restart {
		display: inline-block;
		font-family: 'Ubuntu', sans-serif;
		font-size: 1.2rem;
		line-height: 39px;
		background: #2f2f2f;
		color: #8aa818;
		border: 1px groove #fff;
		border-radius: 5px;
		height: 40px;
		padding: 0 10px;
		text-align: center;
	}

	&__restart {
		cursor: pointer;
		background: rgb(235, 84, 64);
		border: 1px groove #fff;
		color: #f1f1f1;
	}
}
</style>
