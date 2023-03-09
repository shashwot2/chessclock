<script lang="ts">
    let Lcounter = 500;
    let interval: ReturnType<typeof setInterval>;
    let Rcounter = 5;
    function startTimer() {
        interval = setInterval(() => {
            if (Lcounter > 0)
                Lcounter--;
            else if (Lcounter == 0)
                clearInterval(interval)
        }, 1)

    }
</script>

<button on:click={startTimer}>
    {Lcounter} 
</button>

<button>
    white
</button>
