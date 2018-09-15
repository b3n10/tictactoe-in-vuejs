<template>
	<div class="main">
		<div class="board">
			<Box v-for="(box, index) in boxes"
				:text="box.text"
				:key="index"
				:boxKey="index"
				@userMove="userMoveHandler"
				>
			</Box>
		</div>

		<MarkLine
				:mrk="marked"
				:mrkCls="markClass">
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
			boxes: [
				{ text: '' }, { text: '' }, { text: '' },
				{ text: '' }, { text: '' }, { text: '' },
				{ text: '' }, { text: '' }, { text: '' },
			],
			markClass: '',
			letterWin: ''
		}
	},

	components: { Box, MarkLine },

	mounted() {
		if (this.oppFt) this.opponentMove()
	},

	methods: {
		mark(index, letter) {
			if (!this.checkWin() && this.boxes[index].text === '') {
				this.boxes[index].text = letter
			}

			if (this.checkWin()) {
				this.$emit('result', `Game Over! ${this.letterWin} wins!`)
				this.marked = true
				/* start debugging */
				console.log('Winner:', this.markClass, this.letterWin)
				/* end debugging */
			} else if (this.allFilled()) {
				this.$emit('result', 'Draw')
				this.marked = true
			}

			if (this.checkWin() || this.allFilled()) this.$emit('reset')

		},

		userMoveHandler(index) {
			if (!this.checkWin() && this.boxes[index].text === '') {
				this.mark(index, this.usrMk)
				this.opponentMove()
			}
		},

		opponentMove() {
			const slots = [
				/* horizontal */
				[0, 1, 2], [3, 4, 5], [6, 7, 8],
				/* vertical */
				[0, 3, 6], [1, 4, 7], [2, 5, 8],
				/* diagonal */
				[0, 4, 8], [2, 4, 6]
			]

			/* offense */
			if ( slots.some(slot => this.moveCondition(slot, this.oppMk)) ) return
			/* defense */
			if ( slots.some(slot => this.moveCondition(slot, this.usrMk)) ) return

			/* random move */
			do {
				var index = parseInt((Math.random() * 8).toFixed())
			} while (!this.allFilled() && this.boxes[index].text !== '')
			this.opponentMark(index)
		},

		moveCondition(slots, mark) {
			const box = this.boxes
			let mark_count = 0, boxIndex = null

			slots.forEach(slot => {
				if (box[slot].text === mark) mark_count++
				else if (box[slot].text === '') boxIndex = slot
			})

			if (mark_count === 2 && boxIndex !== null) return this.opponentMark(boxIndex)
		},

		opponentMark(boxIndex) {
			if (this.boxes[boxIndex].text === '' && !this.checkWin()) {
				setTimeout(() => this.mark(boxIndex , this.oppMk), 100)
				return true
			}
		},

		allFilled() {
			return this.boxes.filter(b => b.text !== '').length === 9
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
			].some( slot => this.getPattern(slot, letter) )
		},

		getPattern(slot, letter) {
			const [ x, xx, xxx, mark ] = slot
			if ([x, xx, xxx].filter(i => this.boxes[i].text === letter).length === 3) return (this.markClass = mark) && (this.letterWin = letter)
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
	overflow: hidden;

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
