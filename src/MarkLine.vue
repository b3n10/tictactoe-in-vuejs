<template>
	<transition name="mark_slide">
	<div v-show="mrk"
		class="markline"
		:class="this.block + '__' + this.mrkCls">
	</div>
	</transition>
</template>

<script>
export default {
	props: [ 'mrk', 'mrkCls' ],

	data() {
		return {
			block: 'markline'
		}
	}
}
</script>

<style lang="scss">
$line_color: #ad6d00;

.markline {
	position: relative;
	top: -112%;
	left: 47%;
	background: $line_color;

	/* horizontal */
	&__hrt {
		position: absolute;
		top: 14.5%;
		left: 0;
		width: 345px;
		height: 10px;
		border-radius: 5px;
		overflow: hidden;
	}

	&__hrm {
		position: absolute;
		top: 47.9%;
		left: 0;
		width: 345px;
		height: 10px;
		border-radius: 5px;
		overflow: hidden;
	}

	&__hrb {
		position: absolute;
		top: 81.4%;
		left: 0;
		width: 345px;
		height: 10px;
		border-radius: 5px;
		overflow: hidden;
	}

	/* vertical */
	&__vrl {
		position: absolute;
		top: 0.4%;
		left: 14.5%;
		width: 10px;
		height: 345px;
		border-radius: 5px;
		overflow: hidden;
	}

	&__vrm {
		position: absolute;
		top: 0.4%;
		left: 47.5%;
		width: 10px;
		height: 345px;
		border-radius: 5px;
		overflow: hidden;
	}

	&__vrr {
		position: absolute;
		top: 0.4%;
		left: 81.5%;
		width: 10px;
		height: 345px;
		border-radius: 5px;
		overflow: hidden;
	}

	/* diagonal */
	&__dgl {
		width: 10px;
		height: 430px;
		background: transparent;

		&::before {
			content:"";
			border-radius: 5px;
			background: $line_color;
			position: absolute;
			transform: rotate(135deg);
			width: 10px;
			height: 430px;
		}
	}

	&__dgr {
		width: 10px;
		height: 430px;
		background: transparent;

		&::after {
			content:"";
			border-radius: 5px;
			background: $line_color;
			position: absolute;
			right: -20%;
			transform: rotate(45deg);
			width: 10px;
			height: 430px;
		}
	}
}

.mark_slide-enter-active,
.mark_slide-leave-active {
	animation: .5s slidein;
}

@keyframes slidein {
	from { transform: scaleX(0) scaleY(0); }
	to { transform: scaleX(1) scaleY(1); }
}
</style>
