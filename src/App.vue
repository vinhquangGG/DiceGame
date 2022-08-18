<template>

	<div id="app">
		abccccc
		<div class="wrapper clearfix">
            <player v-bind:playerScore="playerScore"
					v-bind:currentScore="currentScore"
					v-bind:status = "status"
			/>
            <controls v-on:changRollDice="handleChangRollDice"
					v-on:handleNewGame="handleNewGame"	
					v-on:handleHoldGame="handleHoldGame"
					v-bind:finalScore="finalScore"
					v-on:handleChangeScore="handleChangeScore"
			/>
            <dice v-bind:dice="dice"	
			/>
			<popup-rule v-bind:guideUp="guideUp"
						v-on:backGuide = "backGuide"
						
			/>
        </div>
	</div>
</template>

<script>
import Player from './components/Player.vue'
import Controls from './components/Controls.vue'
import Dice from './components/Dice.vue'
import PopupRule from './components/PopupRule.vue'
export default {
	name: 'app',
	data () {
		return {
			status: false,
			playerScore: [12,32],
			currentScore: 0,
			dice : [1,1],
			guideUp: 0,
			runGame: 0,
			finalScore: 0
		}
	},
	components: {
		Player,
		Controls,
		Dice,
		PopupRule
	},
	methods: {
		handleChangRollDice(data){
			if(this.runGame === 0){
				alert("Please click new game!")
				return;
			}
			this.dice = [1,1]
			this.dice[0] = data.tmp1;
			this.dice[1] = data.tmp2;
			this.currentScore = this.dice[0]+this.dice[1];
			if(this.dice[0] === 1 || this.dice[1] === 1){
				setTimeout(() => {
					alert(`Người chơi đã xoay vào số 1. Rất tiếc!`)
				}, 10);
				this.status = !this.status;
				this.currentScore = 0
			}
		},
		handleNewGame(){
			this.guideUp = 1
		},
		backGuide(){
			this.guideUp = 0;
			this.runGame = 1;
			this.status = false;
			this.playerScore = [0,0];
			this.dice = [1,1];
			this.currentScore = 0;

		},
		handleHoldGame(){
			// this.playerScore = [0,0];
			let {playerScore, status, currentScore} = this
			let tmp;
			if(status === true){
				tmp = 1;
			}
			else{
				tmp = 0;
			}
			let cloneScore = [...this.playerScore];
			let scoreOld = playerScore[tmp];
			cloneScore[tmp] = scoreOld + currentScore;
			this.playerScore = cloneScore;
			this.changePlayer();
		},
		changePlayer(){
			this.status = !this.status;
			this.currentScore = 0;
		},
		handleChangeScore(e){
			this.finalScore = (parseInt(e.target.value));
		}
	}
}
</script>

<style>
	* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/public/assets/back.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}


</style>
