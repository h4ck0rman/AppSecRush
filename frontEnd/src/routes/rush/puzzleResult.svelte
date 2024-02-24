<script>
    export let results;

    async function emote(result) {
        if (result) {
            res = "✅"
        } else {
            res = "❎"
        }
        return res;
    }
</script>

<div class="container flex flex-row w-full items-start flex-wrap px-10">
    {#each results as result}
        <div class="flex flex-col items-center px-2">
            <p class="text-green-900">{result.result ? "✅" : "❎"}</p>
            <p class="text-white">{result.num}</p>
            
        </div>
    {/each}
</div>
