<template>
	<div>
		<StartButton v-if="showButton"
							 @start="startHandler"
							 >
		</StartButton>

		<Board v-if="play_game"
				 :oppFt="opponentFirst"
				 :usrMk="userMark"
				 :oppMk="opponentMark"
				 @reset="resetHandler"
				 >
		</Board>
	</div>
</template>

<script>
import Board from './Board.vue'
import StartButton from './StartButton.vue'

document.title = 'tic tac toe'

export default {
	name: 'app',
	data() {
		return {
			play_game: false,
			opponentFirst: null,
			userMark: '',
			opponentMark: '',
			showButton: true
		}
	},
	components: { Board, StartButton },
	methods: {
		startHandler(bool) {
			this.opponentFirst = bool
			this.play_game = true
			this.userMark = (this.opponentFirst) ? 'O' : 'X'
			this.opponentMark = (this.opponentFirst) ? 'X' : 'O'
			this.showButton = false
		},
		resetHandler() {
			this.showButton = true
			this.play_game = false
		}
	}
}
</script>

<style lang="scss">
* {
	box-sizing: border-box;
}

body, html {
	padding: 0;
	margin: 0;
}
</style>
