<template>
	<div class="app">
		<StartButton :shwBtn="showButton"
							 :rlt="result"
							 @start="startHandler"
							 @reset="resetNowHandler">
		</StartButton>

		<Board v-if="play_game"
				 :oppFt="opponentFirst"
				 :usrMk="userMark"
				 :oppMk="opponentMark"
				 @result="resultHandler"
				 @reset="resetHandler"
				 @resetNow="resetNowHandler"
				 >
		</Board>
	</div>
</template>

<script>
import StartButton from './StartButton.vue'
// import Results from './Results.vue'
import Board from './Board.vue'

document.title = 'tic tac toe'

export default {
	name: 'app',

	data() {
		return {
			play_game: false,
			opponentFirst: null,
			userMark: '',
			opponentMark: '',
			showButton: 1,
			result: null
		}
	},

	components: { StartButton, Board },

	methods: {
		startHandler(bool) {
			this.opponentFirst = bool
			this.play_game = false
			this.result = null
			document.title = 'tic tac toe'

			setTimeout(() => {
				this.play_game = true
				this.userMark = (this.opponentFirst) ? 'O' : 'X'
				this.opponentMark = (this.opponentFirst) ? 'X' : 'O'
				this.showButton = 0
			}, 0)
		},

		resetNowHandler() {
			this.startHandler(this.opponentFirst)
		},

		resetHandler() {
			this.showButton = 1
		},

		resultHandler(r) {
			this.result = r
			document.title = 'tic tac toe - ' + r
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
	background-color: #1f384d;
}

.app {
	position: relative;
	height: 100vh;
	display: flex;
	flex-direction: column;
	justify-content: center;
	justify-content: space-around;
	align-items: center;
	overflow: hidden;
}

</style>
