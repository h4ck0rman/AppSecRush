<script>
    export let results;
    const correct = "logos/green_tick.png";
    const wrong = "logos/red_cross.png";


</script>

<div class="container flex flex-row w-full items-start flex-wrap px-10">
    {#each results as result}
        <div class="flex flex-col items-center px-2 py-2">
            <img src={result.result ? correct : wrong} alt="result logo" class="w-6"/>
            <p class="text-white font-bold">{result.num}</p>
            
        </div>
    {/each}
</div>
