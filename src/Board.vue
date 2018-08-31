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

	components: { Box },

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
			const horizontal_slots = [ [0, 1, 2], [3, 4, 5], [6, 7, 8] ]
			const vertical_slots = [ [0, 3, 6], [1, 4, 7], [2, 5, 8] ]
			const diagonal_slots = [ [0, 4, 8], [2, 4, 6] ]

			/* offense */
			if (horizontal_slots.some(s => this.moveCondition(s, this.oppMk))) { return }
			else if (vertical_slots.some(s => this.moveCondition(s, this.oppMk))) { return }
			else if (diagonal_slots.some(s => this.moveCondition(s, this.oppMk))) { return }

			/* defense */
			else if (horizontal_slots.some(s => this.moveCondition(s, this.usrMk))) { return }
			else if (vertical_slots.some(s => this.moveCondition(s, this.usrMk))) { return }
			else if (diagonal_slots.some(s => this.moveCondition(s, this.usrMk))) { return }

			/* special move when middle slot is taken */
			else if (this.boxTexts[4].text !== '' && this.boxTexts[8].text === '') { this.opponentMark(8) }

			else {
				do {
					var k = parseInt((Math.random() * 8).toFixed())
				} while (!this.allFilled() && this.boxTexts[k].text !== '')
				this.opponentMark(k)
			}
		},

		moveCondition(s, m) {
			const box = this.boxTexts
			const [x, xx, xxx] = s

			if ([x, xx].filter(i => box[i].text === m).length === 2 && box[xxx].text === '') return this.opponentMark(xxx)
			if ([x, xxx].filter(i => box[i].text === m).length === 2 && box[xx].text === '') return this.opponentMark(xx)
			if ([xx, xxx].filter(i => box[i].text === m).length === 2 && box[x].text === '') return this.opponentMark(x)
			return false
		},

		opponentMark(k) {
			!this.checkWin() && setTimeout(() => this.mark(k , this.oppMk), 100)
			return true
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
.board {
	width: 350px;
	height: 350px;
	padding: 0;
	margin: 100px auto 0 auto;
	use-select: none;
	-moz-user-select: none;
}
</style>
