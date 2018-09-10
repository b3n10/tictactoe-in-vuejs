<template>
	<transition name="mark_slide">
	<div v-if="mrk"
		class="markline"
		:class="this.block + markclass">
	</div>
	</transition>
</template>

<script>
export default {
	props: [ 'mrk' ],

	data() {
		return {
			block: 'markline',
			markclass: '__horizontal-1'
		}
	}
}
</script>

<style lang="scss">
.markline {
	position: absolute;
	background: #c1c1c1;
	border-radius: 5px;
	overflow: hidden;

	$horizontal_width: 345px;
	$horizontal_width_lg: 494px;
	$horizontal_height: 10px;
	$horizontal_height_lg: 20px;

	&__horizontal-1 {
		background: #c19649;
		top: 14.5%;
		left: 0;
		width: $horizontal_width;
		height: $horizontal_height;

		@media (min-width: 500px) {
			& {
				top: 14.4%;
				left: 0;
				width: $horizontal_width_lg;
				height: $horizontal_height_lg;
			}
		}
	}

	&__horizontal-2 {
		background: #c1c1c1;
		top: 47.9%;
		left: 0;
		width: $horizontal_width;
		height: $horizontal_height;

		@media (min-width: 500px) {
			& {
				top: 67.8%;
				left: 0;
				width: $horizontal_width_lg;
				height: $horizontal_height_lg;
			}
		}
	}
}

.mark_slide-enter-active,
.mark_slide-leave-active {
	animation: .5s slidein;
}

@keyframes slidein {
	from { transform: scaleX(0); }
	to { transform: scaleX(1); }
}
</style>
