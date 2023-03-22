<script lang="ts">
	import { onDestroy } from "svelte";


    // This is the total number of time alotted to right and left
    // Player1 is the left player and Player2 is the right player
    let currentplayer: number = 2;
    let Lcounter:number = 10;
    let Rcounter:number = 10;
    let counterID: ReturnType<typeof setInterval>;
    function startstopTimer() {
        clearInterval(counterID)
        counterID = setInterval(() => {
            if ((Lcounter > 0) && (currentplayer == 1)) {
                Lcounter--;
            }
            else if ((Lcounter > 0) && (currentplayer == 2)) {
                Rcounter--;
            }
            else if (Lcounter == 0) {
                clearInterval(counterID)
                alert("Time is up! right wins!")
                return                
            }
            else if (Rcounter == 0) {
                clearInterval(counterID)
                alert("Time is up! left wins!")
                return
            }
        }, 1000)
        switchPlayers();
    }
    function switchPlayers() {
        if (currentplayer == 1) {
            currentplayer = 2;
        }
        else if (currentplayer == 2) {
            currentplayer = 1;
        }
    }

    onDestroy(() => {
        clearInterval(counterID);
    });
</script>

<button on:click={startstopTimer}>
    {Lcounter} 
</button>

<button on:click={startstopTimer}>
    {Rcounter}
</button>
