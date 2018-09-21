<template>
	<div class="app">
		<StartButton :shwBtn="showButton"
			:rlt="result"
			:play="play_game"
			:frt_run="first_run"
			@start="startHandler"
			@resetNow="resetNowHandler">
		</StartButton>

		<Board v-if="play_game"
				 :oppFt="opponentFirst"
				 :usrMk="userMark"
				 :oppMk="opponentMark"
				 @result="resultHandler"
				 @reset="resetHandler"
				 @resetNow="resetNowHandler">
		</Board>
	</div>
</template>

<script>
import StartButton from './StartButton.vue'
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
			showButton: !!true,
			result: null,
			first_run: true
		}
	},

	components: { StartButton, Board },

	methods: {
		startHandler(bool) {
			this.opponentFirst = bool
			this.play_game = false
			this.result = null
			this.first_run = false
			document.title = 'tic tac toe'

			setTimeout(() => {
				this.play_game = true
				this.userMark = (this.opponentFirst) ? 'O' : 'X'
				this.opponentMark = (this.opponentFirst) ? 'X' : 'O'
				this.showButton = false
			}, 0)
		},

		resetNowHandler() {
			this.startHandler(this.opponentFirst)
		},

		resetHandler() {
			this.showButton = true
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
	align-items: center;
	overflow: hidden;
}

</style>
