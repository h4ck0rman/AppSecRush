<script>
    // Components imported
    import PuzzleResult from "./puzzleResult.svelte";
    import MonacoBox from "./monacoBox.svelte";

    const profile = "h4ck0rLogo.png";
    
    // state for active puzzle rush session UI
    export let rushActive = false;
    const toggleStart = () => {
        rushActive = !rushActive;
        newPuzzle()
    }

    // Example function to substitute for backend response
    let puzzles = [];
    let count = 0;
    
    
    const solvePuzzle = () => {   
        count += 1;
        let results = {num: count, result:((count % 2) == 0)};

        puzzles.push(results);
        puzzles = puzzles;

        newPuzzle()
    }

    let codeUpdate;
    let code = 'import requests;';
    let language = 'python';
    const newPuzzle = () => {
        // get the next puzzle from backend api

        // reflect the next puzzle in the monaco editor
        codeUpdate(code, language);
    }

    
</script>


<div class='flex flex-row w-screen h-screen rounded-lg'>
    <div class="absolute top-0 left-0 py-10 px-10">
        <a href="/">
            <p class="text-3xl text-white font-bold">{'←'}</p>
        </a>
    </div>

    <span class='basis-1/4'>
        <div class="container flex flex-col space-y-10 py-10 bg-zinc-900 h-full">
            <img src={profile} alt="profile of user" class="w-24 py-10 mx-auto"/>
        
            {#if !rushActive}
            <button on:click={toggleStart} class=" mx-auto bg-transparent hover:bg-white text-white font-semibold hover:text-black py-2 px-4 border border-white hover:border-transparent rounded">Start Rush</button>
            
            {:else}
            <div>
                <form class="px-10 py-10 mx-auto flex flex-col">
                    <label for="number-input" class="block mb-2 text-gray-900 dark:text-white font-bold text-sm uppercase">Vulnerable Line Number</label>
                    <input type="number" id="number-input" aria-describedby="helper-text-explanation" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="0" />
                    <button on:click={solvePuzzle} class="bg-transparent hover:bg-white text-white font-semibold hover:text-black py-2 my-2 px-4 border border-white hover:border-transparent rounded">Submit</button>
                </form>
                <PuzzleResult results={puzzles} />
            </div>
            {/if}

        </div>      
    </span>


    <span class='basis-3/4'><MonacoBox bind:updateContent={codeUpdate}/></span>


</div>
