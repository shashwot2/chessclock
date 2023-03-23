<script lang="ts">
	import { onDestroy } from 'svelte';
	import {convertSecToMin} from './utils/secondstominutes.svelte';
	// This is the total number of time alotted to right and left
	// Player1 is the left player and Player2 is the right player
	// Timer's are allotted in seconds
	let currentplayer: number = 2;
	let LeftPTimer: number = 600; //5 Minutes
	let RightPTimer: number = 600;
	//IntervalID is the ID of the timer that subtracts time from the player timers
	let intervalID: ReturnType<typeof setInterval>;
	function startstopTimer() {
		clearInterval(intervalID);
		intervalID = setInterval(() => {
			if (LeftPTimer > 0 && currentplayer == 1) {
				LeftPTimer--;
			} else if (RightPTimer > 0 && currentplayer == 2) {
				RightPTimer--;
			} else if (LeftPTimer == 0) {
				clearInterval(intervalID);
				alert('Time is up! right wins!');
				return;
			} else if (RightPTimer == 0) {
				clearInterval(intervalID);
				alert('Time is up! left wins!');
				return;
			}
		}, 1000);
		switchPlayers();
	}
	function switchPlayers() {
		if (currentplayer === 1) {
			currentplayer = 2;
		} else if (currentplayer === 2) {
			currentplayer = 1;
		}
	}

	onDestroy(() => {
		clearInterval(intervalID);
	});
</script>

<div class="container">
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<div class="clock {currentplayer === 1 ? 'active' : ''}"
		on:click={startstopTimer}>
		{convertSecToMin(LeftPTimer)}
		</div>
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<div class="clock {currentplayer === 2 ? 'active' : ''}"
		on:click={startstopTimer}>
		{convertSecToMin(RightPTimer)}
		</div>
</div>

<style>
	.container {
		display: flex;
		justify-content: space-around;
		align-items: center;
		height: 100%;
		width: 100%;
	}
	.clock {
		font-size: 5rem;
		border: 1px solid black;
		border-radius: 50%;
		width: 20rem;
		height: 20rem;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.clock.active {
		background-color: red;
	}
</style>