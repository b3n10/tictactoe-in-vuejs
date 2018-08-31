<template>
	<div class="box"
			:class="boxCls"
			@click="$emit('userMove', boxKey)"
			>
			<p class="box__text"
			:class="txtCls"
			>
			{{ text }}
			</p>
	</div>
</template>

<script>
export default {
	props: ['text', 'boxKey', 'boxCls', 'txtCls'],
}
</script>

<style lang="scss">
.box {
	width: 33.3%;
	height: 33%;
	display: inline-block;
	border-right: 5px solid #000;
	border-bottom: 5px solid #000;
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
		color: black;
		background-color: yellow;
	}

	&__text {
		width: 100%;
		height: 100%;
		margin: 0;
		padding: 0;
		font-weight: 900;
		font: 110px/1.01 serif;
		overflow: hidden;
		cursor: pointer;
		opacity: 0;
		transition: opacity 1s;

		&.marked {
			opacity: 1;
		}
	}
}
</style>
