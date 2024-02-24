<script lang="ts">
    import { onDestroy, onMount } from 'svelte';
    import type * as Monaco from 'monaco-editor/esm/vs/editor/editor.api';

    let editor: Monaco.editor.IStandaloneCodeEditor;
    let monaco: typeof Monaco;
    let editorContainer: HTMLElement;

    onMount(async () => {
        // Import our 'monaco.ts' file here
        // (onMount() will only be executed in the browser, which is what we want)
        monaco = (await import('./monaco')).default;

        const code = `
from flask import Flask, request, send_file
from jinja2 import Environment
import pdfkit
import os

app = Flask(__name__)

@app.route('/generate_pdf', methods=['POST'])
def generate_pdf():
    data = request.json
    html_template = data.get('html_template', '')
    user_data = data.get('user_data', {})
    
    # Initialize a Jinja2 environment
    env = Environment()

    # load the template into the environment 
    template = env.from_string(html_template)

    # Render the template with user_data
    rendered_html = template.render(user_data)
    
    # Convert HTML to PDF
    pdf_path = '/tmp/output.pdf'
    pdfkit.from_string(rendered_html, pdf_path)
    
    # Send the generated PDF back to the client
    return send_file(pdf_path, attachment_filename='output.pdf')

if __name__ == '__main__':
    app.run(debug=True)

        `

        // Your monaco instance is ready, let's display some code!
        const editor = monaco.editor.create(editorContainer);
        const model = monaco.editor.createModel(
            code,
            "python",
        );
        editor.setModel(model);
        monaco.editor.setTheme('vs-dark')
    });

    onDestroy(() => {
        monaco?.editor.getModels().forEach((model) => model.dispose());
        editor?.dispose();
    });
</script>

<div class="flex items-center bg-zinc-900 h-full">

    <div class="w-full h-full text-lg" bind:this={editorContainer} />
</div>
