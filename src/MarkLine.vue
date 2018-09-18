<template>
	<transition name="mark_slide">
		<div
		v-if="mrk"
		class="markline"
		:class="this.block + '__' + this.mrkCls"
		@click="$emit('resetFromMarkLine')"
		 >
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
$line_color: #e59044;

.markline {
	position: relative;
	background: $line_color;
	border-radius: 10px;
	cursor: pointer;

	/* horizontal */
	&__hrt {
		position: absolute;
		top: 14.5%;
		left: 0;
		width: 345px;
		height: 10px;
	}

	&__hrm {
		position: absolute;
		top: 47.9%;
		left: 0;
		width: 345px;
		height: 10px;
	}

	&__hrb {
		position: absolute;
		top: 81.4%;
		left: 0;
		width: 345px;
		height: 10px;
	}

	/* vertical */
	&__vrl {
		position: absolute;
		top: 0.4%;
		left: 14.5%;
		width: 10px;
		height: 345px;
	}

	&__vrm {
		position: absolute;
		top: 0.4%;
		left: 47.5%;
		width: 10px;
		height: 345px;
	}

	&__vrr {
		position: absolute;
		top: 0.4%;
		left: 81.0%;
		width: 10px;
		height: 345px;
	}

	/* diagonal */
	&__dgl {
		top: -111%;
		left: 48%;
		width: 10px;
		height: 430px;
		background: transparent;

		&::before {
			content:"";
			background: $line_color;
			position: absolute;
			transform: rotate(135deg);
			width: 10px;
			height: 430px;
			border-radius: 10px;
		}
	}

	&__dgr {
		top: -111%;
		left: 46.8%;
		width: 10px;
		height: 430px;
		background: transparent;

		&::before {
			content:"";
			background: $line_color;
			position: absolute;
			transform: rotate(45deg);
			width: 10px;
			height: 430px;
			border-radius: 10px;
		}
	}

	@media (min-width: 500px) {
		&__hrt,
		&__hrm,
		&__hrb {
			width: 497px;
			height: 15px;
		}

		&__vrl,
		&__vrm,
		&__vrr {
			width: 15px;
			height: 491px;
		}

		&__dgl {
			left: 48%;
		}
		&__dgr {
			left: 47%;
		}
		&__dgl,
		&__dgr {
			top: -112%;
			width: 15px;
			height: 620px;
			background: transparent;

			&::before {
				width: 15px;
				height: 620px;
			}
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
