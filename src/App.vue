<template>
	<Board :oppFt="opponentFirst"
	:usrMk="userMark"
	:oppMk="opponentMark"
	>
	</Board>
</template>

<script>
import Board from './Board.vue'

export default {
	name: 'app',
	data() {
		return {
			opponentFirst: true,
			userMark: '',
			opponentMark: ''
		}
	},
	components: {
		Board
	},
	mounted() {
		document.title = 'tic tac toe'
		this.userMark = (this.opponentFirst) ? 'O' : 'X'
		this.opponentMark = (this.opponentFirst) ? 'X' : 'O'
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
