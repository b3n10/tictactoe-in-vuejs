<template>
	<div class="boxDiv"
			:class="boxCls"
			@click="$emit('userMove', boxKey)"
			>
			<p class="pDiv"
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
.boxDiv {
	width: 32%;
	height: 32%;
	margin: 2px 3px;
	padding: 0;
	display: inline-block;
	border: 1px dashed #000;
	box-sizing: border-box;
	text-align: center;
	overflow: hidden;
	cursor: pointer;
}
.boxDiv.marked {
	color: black;
	background-color: yellow;
}
p.pDiv {
	width: 100%;
	height: 100%;
	margin: 0;
	font-weight: 900;
	font: 150px/1.03 serif;
	overflow: hidden;
	cursor: pointer;
	opacity: 0;
	transition: opacity 1s;
}
p.marked {
	opacity: 1;
}
</style>
