<template>
	<div id="app">
		<h1>Street Fighter</h1>
		<div class="fighters row">
			<div class="player figher column">
				<span class="fighter-name">Player 1</span>
				<health-meter :meter-width="playerHealth"></health-meter>
				{{playerHealth}}
			</div>
			<div class="opponent fighter column">
				<span class="fighter-name">Opponent</span>
				<health-meter :meter-width="opponentHealth"></health-meter>
				{{opponentHealth}}
			</div>
		</div>
		<div class="row">
			<div class="column">
				<custom-button :button-style="'green'" @pressed="handleAttackButton"></custom-button>
				<custom-button :button-style="'red'" @pressed="handleSpecialAttackButton"></custom-button>
				<button id="show-modal" @click="this.showModal = true">Show Modal</button>
			</div>
			<div class="column">
				<log :messages="messageLog"></log>
			</div>
		</div>
		<modal  v-show="showModal"></modal>
		<!-- modal -->
			<!-- Game over text -->
			<!-- Button (plain) -->
		<!--/ modal -->
	</div>
</template>

<script>

import CustomButton from './components/Button';
import HealthMeter from './components/HealthMeter';
import Modal from './components/Modal';
import Log from './components/Log';

export default {
	data() {
		return {
			playerHealth: 100,
			opponentHealth: 100,
			messageLog: [],
			showModal: false,
			gameInPlay: true,
			gameOverMessage: "",
			theWinner: ""
		}
	},
	methods: {
		getRandomDamageAmount: function(min, max) {
			return Math.floor(Math.random() * (max - min + 1)) + min;
		},
		handleAttackButton: function(){
			let opponentDamage = this.getRandomDamageAmount(5,9);
			this.opponentHealth = this.opponentHealth - opponentDamage;
			this.messageLog.push(`Player used Attack and did ${opponentDamage} damage.`);
			let playerDamage = this.getRandomDamageAmount(5,9);
			this.playerHealth = this.playerHealth - playerDamage;
			this.messageLog.push(`Opponent attacks and does ${playerDamage} damage.`);
			this.handleScoreKeeping();
		},
		handleSpecialAttackButton: function(){
			let opponentDamage = this.getRandomDamageAmount(8,12);
			this.opponentHealth = this.opponentHealth - opponentDamage;
			this.messageLog.push(`Player used Special Attack and did ${opponentDamage} damage.`);
			let playerDamage = this.getRandomDamageAmount(8,12);
			this.playerHealth = this.playerHealth - playerDamage;
			this.messageLog.push(`Opponent attacks and does ${playerDamage} damage.`); 
			this.handleScoreKeeping();
		},
		handleScoreKeeping: function(){
			if (this.playerHealth < 1 || this.opponentHealth < 1) {
				if (this.playerHealth >= this.opponentHealth) {
					this.theWinner = "Player"
				} else {
					this.theWinner = "Opponent"
				}
				
				this.handleGameOver();
			} 
		},
		handleGameOver: function(){
			//this.showModal = true;
			this.gameInPlay = false;
			this.showModal = true;
			this.gameOverMessage = `Game Over, Man! ${this.theWinner} wins. Play again?`;
			//alert(this.gameOverMessage);
		}
	},
	components: {
		CustomButton,
		Log,
		HealthMeter,
		Modal
	}
}
</script>

<style lang="scss">
#app {
	font-family: Arial, Helvetica, sans-serif;
}
h1 {
	font-size: 48px;
	font-weight: normal;
	margin-bottom: 30px;
	text-align: center;
}
.row {
	display: flex;
	margin: 0 auto;
	max-width: 900px;
	.column {
		flex: 1 0 50%;
		padding: 0 10px;
	}
}

.fighters {
	margin-bottom: 50px;
}
</style>
