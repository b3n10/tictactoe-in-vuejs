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
.markline {
	position: relative;

	/* horizontal */
	$horizontal_width: 345px;
	$horizontal_width_lg: 494px;
	$horizontal_height: 10px;
	$horizontal_height_lg: 20px;

	&__hrt {
		position: absolute;
		background: #c19649;
		border-radius: 5px;
		overflow: hidden;

		top: 14.5%;
		left: 0;
		width: 345px;
		height: 10px;
	}

	&__hrm {
		position: absolute;
		background: #c19649;
		border-radius: 5px;
		overflow: hidden;

		top: 47.9%;
		left: 0;
		width: 345px;
		height: 10px;
	}

	&__hrb {
		position: absolute;
		background: #c19649;
		border-radius: 5px;
		overflow: hidden;

		top: 81.4%;
		left: 0;
		width: 345px;
		height: 10px;
	}

	/* vertical */
	$vertical_width: 10px;
	$vertical_height: 345px;
	$vertical_width_lg: 494px;
	$vertical_height_lg: 20px;
	$vertical_top: 0.4%;

	&__vrl {
		position: absolute;
		background: #c19649;
		border-radius: 5px;
		overflow: hidden;

		top: 0.4%;
		left: 14.5%;
		width: 10px;
		height: 345px;
	}

	&__vrm {
		position: absolute;
		background: #c19649;
		border-radius: 5px;
		overflow: hidden;

		top: 0.4%;
		left: 47.5%;
		width: 10px;
		height: 345px;
	}

	&__vrr {
		position: absolute;
		background: #c19649;
		border-radius: 5px;
		overflow: hidden;

		top: 0.4%;
		left: 81.5%;
		width: 10px;
		height: 345px;
	}

	/* diagonal */
	$vertical_height: 430px;

	&__dgl {
		width: 10px;
		height: 430px;
		background: transparent;

		&::before {
			content:"";
			position: absolute;
			top: -393px;
			left: 164px;
			border-radius: 5px;
			background: #c19649;
			width: 10px;
			height: 430px;
			transform: rotate(135deg);
		}
	}

	&__dgr {
		width: 10px;
		height: 430px;
		background: transparent;

		&::before {
			content:"";
			position: absolute;
			top: -393px;
			left: 167px;
			border-radius: 5px;
			background: #c19649;
			width: 10px;
			height: 430px;
			transform: rotate(45deg);
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
