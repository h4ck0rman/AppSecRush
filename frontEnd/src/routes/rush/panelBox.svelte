<script>
    import PuzzleResult from "./puzzleResult.svelte";

    const profile = "h4ck0rLogo.png";


    let rushActive = false;

    const toggleStart = () => {
        rushActive = !rushActive;
    }

    let puzzles = [];
    let count = 0;
    const solvePuzzle = () => {
        count += 1;
        let results = {num: count, result:((count % 2) == 0)};

        console.log(results)
        puzzles.push(results);
        puzzles = puzzles;

        console.log(puzzles)
    }

</script>


<div class="flex flex-col space-y-10 items-center py-10 bg-zinc-900 h-full">
    <img src={profile} alt="profile of user" class="w-24"/>

    {#if !rushActive}

    <button on:click={toggleStart} class="bg-transparent hover:bg-white text-white font-semibold hover:text-black py-2 px-4 border border-white hover:border-transparent rounded">Start Rush</button>
    
    {:else}

    <form>
        <label for="number-input" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Vulnerable Code Line Number</label>
        <input type="number" id="number-input" aria-describedby="helper-text-explanation" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="0" />
        <button on:click={solvePuzzle} class="bg-transparent hover:bg-white text-white font-semibold hover:text-black py-2 my-2 px-4 border border-white hover:border-transparent rounded">Submit</button>
    </form>
    <PuzzleResult results={puzzles} />
    
    {/if}
</div>  