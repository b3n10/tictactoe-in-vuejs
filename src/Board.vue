<template>
	<div class="board">
		<Box v-for="(b, index) of boxTexts"
			 :text="b.text"
			 :key="index"
			 :boxKey="index"
			 :boxCls="b.boxClass"
			 :txtCls="b.textClass"
			 @userMove="userMoveHandler"
			 >
		</Box>
	</div>
</template>

<script>
import Box from './Box.vue'
import Vue from 'vue'

export default {
	name: 'board',
	props: ['oppFt', 'usrMk', 'oppMk'],
	data() {
		return {
			boxTexts: [
				{text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''},
				{text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''},
				{text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''},
			],
		}
	},
	components: {
		Box
	},
	mounted() {
		if (this.oppFt) this.opponentMove()
	},
	methods: {
		mark(k, l) {
			if (!this.checkWin() && this.boxTexts[k].text === '') {
				this.boxTexts[k].text = l
				this.boxTexts[k].textClass = 'marked'
			}

			if (this.checkWin()) this.$emit('result', `Game Over! ${this.checkWin()} wins!`)
			else if (this.allFilled()) this.$emit('result', 'Draw')

			if (this.checkWin() || this.allFilled()) this.$emit('reset')
		},
		userMoveHandler(k) {
			if (!this.checkWin() && this.boxTexts[k].text === '') {
				this.mark(k, this.usrMk)
				this.boxTexts[k].boxClass = 'marked'
				this.opponentMove()
			}
		},
		opponentMove() {
			do {
				var k = parseInt((Math.random() * 8).toFixed())
			} while (!this.allFilled() && this.boxTexts[k].text !== '')
			!this.checkWin() && setTimeout(() => this.mark(k , this.oppMk), 180)
		},
		allFilled() {
			let filledCount = 0
			this.boxTexts.forEach(b => b.text !== '' && (filledCount++))
			return filledCount === 9
		},
		checkWin() {
			return ['X', 'O'].map(l => this.patterns(l)).filter(item => item)[0];
		},
		patterns(l) {
			const box = this.boxTexts

			if (
				/* horizontal pattern */
				([0, 1, 2].filter(i => box[i].text === l).length === 3) ||
				([3, 4, 5].filter(i => box[i].text === l).length === 3) ||
				([6, 7, 8].filter(i => box[i].text === l).length === 3) ||

				/* vertical pattern */
				([0, 3, 6].filter(i => box[i].text === l).length === 3) ||
				([1, 4, 7].filter(i => box[i].text === l).length === 3) ||
				([2, 5, 8].filter(i => box[i].text === l).length === 3) ||

				/* diagonal pattern */
				([0, 4, 8].filter(i => box[i].text === l).length === 3) ||
				([6, 4, 2].filter(i => box[i].text === l).length === 3)
			) return l

			return false
		}
	}
}
</script>

<style lang="scss">
$board_size: 500px;

.board {
	width: $board_size;
	height: $board_size;
	border-radius: 5px;
	padding: 5px;
	margin: 80px auto;
	use-select: none;
	-moz-user-select: none;
}
</style>
