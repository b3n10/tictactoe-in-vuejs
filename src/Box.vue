<template>
	<div class="box"
			:class="boxCls"
			@click="$emit('userMove', boxKey)"
			>

			<transition name="fade">
				<p v-if="text === 'X'" class="box__text" :class="txtCls">
					<span class="box__text-x1"></span>
					<span class="box__text-x2"></span>
				</p>
				<p v-if="text === 'O'" class="box__text" :class="txtCls">
					{{ text }}
				</p>
			</transition>
	</div>
</template>

<script>
export default {
	props: ['text', 'boxKey', 'boxCls', 'txtCls'],
}
</script>

<style lang="scss">
.box {
	background-color: #f1f1f1;
	width: 33%;
	height: 33%;
	display: inline-block;
	border-right: 5px solid #000;
	border-bottom: 5px solid #000;
	border-radius: 5px;
	box-sizing: border-box;
	text-align: center;
	overflow: hidden;
	cursor: pointer;
	vertical-align: top;

	&:nth-child(3n+3) {
		border-right: none;
	}

	&:nth-last-child(-n+3) {
		border-bottom: none;
	}

	&.marked {
		color: #000;
	}

	&__text {
		position: relative;
		width: 100%;
		height: 100%;
		margin: 0;
		padding: 0;
		font-weight: 900;
		font: 110px/1.01 serif;
		overflow: hidden;
		cursor: pointer;

		&-x1 {
			transform: rotate(45deg);
		}
		&-x2 {
			transform: rotate(135deg);
		}

		&-x1, &-x2 {
			position: absolute;
			top: 12%;
			left: 45%;
			width: 10px;
			height: 80%;
			background-color: #565454;
			border-radius: 5px;
			// transition: width .5s;

			@media (min-width: 500px) {
				& {
					top: 8%;
					width: 15px;
					height: 86%;
				}
			}
		}

	}
}

.fade-enter-active,
.fade-leave-active {
	animation: bounce-in .5s;
}

/*
.fade-enter-active .box__text-x1,
.fade-enter-active .box__text-x2,
.fade-leave-active .box__text-x1,
.fade-leave-active .box__text-x2 {
}

.fade-enter .box__text-x1,
.fade-enter .box__text-x2,
.fade-leave-to .box__text-x1,
.fade-leave-to .box__text-x2 {
	width: 0px;
}
*/

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
