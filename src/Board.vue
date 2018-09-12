<template>
	<div class="main">
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

		<MarkLine
				:mrk="marked"
				:mrkCls="markclass">
		</MarkLine>
	</div>
</template>

<script>
import Box from './Box.vue'
import MarkLine from './MarkLine.vue'

export default {
	name: 'board',

	props: ['oppFt', 'usrMk', 'oppMk'],

	data() {
		return {
			marked: false,
			boxTexts: [
				{text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''},
				{text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''},
				{text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''}, {text: '', boxClass: '', textClass: ''},
			],
			markclass: '',
			letterWin: ''
		}
	},

	components: { Box, MarkLine },

	mounted() {
		if (this.oppFt) this.opponentMove()
	},

	methods: {
		mark(k, l) {
			if (!this.checkWin() && this.boxTexts[k].text === '') {
				this.boxTexts[k].text = l
				this.boxTexts[k].textClass = 'marked'
			}

			if (this.checkWin()) {
				this.$emit('result', `Game Over! ${this.letterWin} wins!`)
				this.marked = true
				/* start debugging */
				console.log('Winner:', this.markclass, this.letterWin)
				/* end debugging */
			} else if (this.allFilled()) {
				this.$emit('result', 'Draw')
				this.marked = true
			}

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

			if (horizontal_slots.some(s => this.moveCondition(s, this.oppMk))) { return }
			else if (horizontal_slots.some(s => this.moveCondition(s, this.usrMk))) { return }

			else if (diagonal_slots.some(s => this.moveCondition(s, this.oppMk))) { return }
			else if (diagonal_slots.some(s => this.moveCondition(s, this.usrMk))) { return }

			else if (vertical_slots.some(s => this.moveCondition(s, this.oppMk))) { return }
			else if (vertical_slots.some(s => this.moveCondition(s, this.usrMk))) { return }

			else {
				do {
					var k = parseInt((Math.random() * 8).toFixed())
				} while (!this.allFilled() && this.boxTexts[k].text !== '')
				this.opponentMark(k)
			}
		},

		moveCondition(s, m) {
			const box = this.boxTexts

			let countM = 0, k = null

			s.forEach(s => {
				if (box[s].text === m) countM++
				else if (box[s].text === '') k = s
			})

			if (countM === 2 && k !== null) return this.opponentMark(k)

			/*
			const k = s.filter(i => box[i].text !== m && box[i].text === '')
			if (k.length === 1) return this.opponentMark(k[0])
			*/

			/*
			const [x, xx, xxx] = s
			if ([x, xx].filter(i => box[i].text === m).length === 2 && box[xxx].text === '') return this.opponentMark(xxx)
			if ([x, xxx].filter(i => box[i].text === m).length === 2 && box[xx].text === '') return this.opponentMark(xx)
			if ([xx, xxx].filter(i => box[i].text === m).length === 2 && box[x].text === '') return this.opponentMark(x)
			*/
		},

		opponentMark(k) {
			if (this.boxTexts[k].text === '' && !this.checkWin()) {
				setTimeout(() => this.mark(k , this.oppMk), 100)
				return true
			}
		},

		allFilled() {
			return this.boxTexts.filter(b => b.text !== '').length === 9
		},

		checkWin() {
			return ['X', 'O'].map(letter => this.patterns(letter)).includes(true)
		},

		patterns(letter) {
			/*
			hrt: horizontal top
			hrm: horizontal middle
			hrb: horizontal bottom
			 */
			return [
				[0, 1, 2, 'hrt'],
				[3, 4, 5, 'hrm'],
				[6, 7, 8, 'hrb'],

				[0, 3, 6, 'vrl'],
				[1, 4, 7, 'vrm'],
				[2, 5, 8, 'vrr'],

				[0, 4, 8, 'dgl'],
				[6, 4, 2, 'dgr'],
			].some( array => this.getPattern(array, letter) )

			/*
			const vertical = [
				[0, 3, 6, 'vrl'],
				[1, 4, 7, 'vrm'],
				[2, 5, 8, 'vrr']
			].some( array => this.getPattern(array, letter) )

			const diagonal = [
				[0, 4, 8, 'dl'],
				[6, 4, 2, 'dr'],
			].some( array => this.getPattern(array, letter) )

			if (horizontal) {
				console.log(horizontal, 'h')
				return horizontal
			}
			if (vertical) {
				console.log(vertical, 'v')
				return vertical
			}
			if (diagonal) {
				console.log(diagonal, 'd')
				return diagonal
			}
			*/
			/*
			if (horizontal) return horizontal
			if (vertical) return vertical
			if (diagonal) return diagonal
			*/

			/*
			if (
				([0, 1, 2].filter(i => box[i].text === letter).length === 3) ||
				([3, 4, 5].filter(i => box[i].text === letter).length === 3) ||
				([6, 7, 8].filter(i => box[i].text === letter).length === 3) ||

				([0, 3, 6].filter(i => box[i].text === letter).length === 3) ||
				([1, 4, 7].filter(i => box[i].text === letter).length === 3) ||
				([2, 5, 8].filter(i => box[i].text === letter).length === 3) ||

				([0, 4, 8].filter(i => box[i].text === letter).length === 3) ||
				([6, 4, 2].filter(i => box[i].text === letter).length === 3)
			) return l
			*/
		},

		getPattern(array, letter) {
			const [ x, xx, xxx, mark ] = array
			if ([x, xx, xxx].filter(i => this.boxTexts[i].text === letter).length === 3) return (this.markclass = mark) && (this.letterWin = letter)
		}
	}
}
</script>

<style lang="scss">
.main {
	position: relative;
	width: 350px;
	height: 350px;
	padding: 0;
	margin: 100px auto 0 auto;

	@media (min-width: 500px) {
		& {
			width: 500px;
			height: 500px;
		}
	}
}

.board {
	width: 100%;
	height: 100%;
	use-select: none;
	-moz-user-select: none;
}
</style>
