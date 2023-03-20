<script lang="ts">
    // This is the total number of time allotted to right and left
    let Lcounter:number = 10;
    // let Rcounter:number = 10;
    let LcounterID: ReturnType<typeof setInterval>;
    function startTimer() {
        LcounterID = setInterval(() => {
            if (Lcounter > 0) {
                Lcounter--;
            }
            else if (Lcounter == 0) {
                clearInterval(LcounterID)
                alert("Time is up!")                
            }
        }, 1000)

    }
</script>

<button on:click={startTimer}>
    {Lcounter} 
</button>

<button>
    white
</button>
