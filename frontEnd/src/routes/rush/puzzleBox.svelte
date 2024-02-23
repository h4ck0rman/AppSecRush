<script>
    import SvelteMarkdown from 'svelte-markdown'
    import Highlight, { LineNumbers } from "svelte-highlight";
    import php from "svelte-highlight/languages/php";

    let code = "<?php echo ' & <br /> '.$contact->getField('nameLast') ;?>"

</script>

<div class="container flex flex-col items-center py-10 bg-zinc-900 h-full">
    <h1 class="uppercase text-3xl font-semibold text-white">Puzzle Box</h1>
    <Highlight language={php} {code} let:highlighted>
        <LineNumbers {highlighted} />
    </Highlight>
</div>
