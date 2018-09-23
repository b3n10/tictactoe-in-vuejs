<template>
	<div class="btn">
		<transition name="letter_pop">
			<div v-if="shwBtn" class="btn__x" @click="$emit('start', false)">
				X
			</div>
		</transition>
		<div v-if="frt_run" class="btn__vs">
			vs
		</div>
		<div v-if="rlt" class="btn__result">
			{{ rlt }}
		</div>
		<div v-if="play && !rlt" class="btn__restart" @click="$emit('resetNow')">
			R E S E T
		</div>
		<transition name="letter_pop">
			<div v-if="shwBtn" class="btn__o" @click="$emit('start', true)">
				O
			</div>
		</transition>
	</div>
</template>

<script>
export default {
	props: [ 'shwBtn', 'rlt', 'play', 'frt_run' ]
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Ubuntu:700');

.btn {
	font-family: 'Ubuntu', sans-serif;
	margin: 50px auto;
	display: flex;
	height: 0;
	width: 300px;
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
		background: #555;
		color: #f1f1f1;
		font-weight: 900;
		font-size: 5rem;
		line-height: 80px;
		height: 80px;
		width: 80px;
		text-align: center;
		border-radius: 5px;
		cursor: pointer;
	}

	&__vs {
		display: inline-block;
		font-size: 2rem;
		line-height: 39px;
		background: #f1f1f1;
		border-radius: 5px;
		color: #2f2f2f;
		height: 39px;
		padding: 0 10px;
		text-align: center;
	}

	&__result,
	&__restart {
		display: inline-block;
		font-size: 1.5rem;
		line-height: 40px;
		background: #2f2f2f;
		color: #f1f1f1;
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

.letter_pop-enter-active {
	animation: bounce-in .5s;
}
.letter_pop-leave-active {
	opacity: 0;
}
@keyframes bounce-in {
	0% {
		transform: scale(0);
	}
	50% {
		transform: scale(1.5);
	}
	100% {
		transform: scale(1);
	}
}
</style>
