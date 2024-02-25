<script>
    import PanelBox from "./panelBox.svelte";
    import MonacoBox from "./monacoBox.svelte";

    let rushActive = false;
</script>

<div class='flex flex-row w-screen h-screen rounded-lg'>
    <span class='basis-1/4'><PanelBox bind:rushActive = {rushActive}/></span>
    {#if rushActive}
    <span class='basis-3/4'><MonacoBox /></span>
    {:else}
    <span class='basis-3/4'><p>Loading ...</p></span>
    {/if}
</div>