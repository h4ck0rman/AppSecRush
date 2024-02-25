<script lang="ts">
    export let code = 'Loading ...';
    export let language = 'python';
    
    import { onDestroy, onMount } from 'svelte';
    import type * as Monaco from 'monaco-editor/esm/vs/editor/editor.api';

    let editor: Monaco.editor.IStandaloneCodeEditor;
    let monaco: typeof Monaco;
    let editorContainer: HTMLElement;

    onMount(async () => {
        // Import our 'monaco.ts' file here
        // (onMount() will only be executed in the browser, which is what we want)
        monaco = (await import('./monaco')).default;

        editorContainer["readOnly"] = true;
        // monaco instance is ready, let's display some code!

        const editor = monaco.editor.create(editorContainer, {
            value: code,
            language: language,
            readOnly: true,
            theme: 'vs-dark'
        });
    });

    
    onDestroy(() => {
        editor?.dispose();
    });
</script>

<div class="flex items-center bg-zinc-900 h-full">
    <div class="w-full h-full text-lg" bind:this={editorContainer} />
</div>

