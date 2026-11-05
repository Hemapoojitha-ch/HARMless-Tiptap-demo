<script>
  import '#lib/style.css'
  import { onMount } from 'svelte'
  import { Editor } from '@tiptap/core'
  import StarterKit from '@tiptap/starter-kit'

  let element = $state()
  /** @type {Editor} */
  let editor
  let jsonText = $state('')
  let error = $state('')

  onMount(() => {
    editor = new Editor({
      element,
      extensions: [StarterKit],
      content: '<h2>My note</h2><p>This is <em>italic</em> and this is <strong>bold</strong>.</p>',
    })

    return () => editor.destroy()
  })

  function getJSON() {
    const json = editor.getJSON()
    jsonText = JSON.stringify(json, null, 2)
    error = ''
  }

  function loadJSON() {
    try {
      const json = JSON.parse(jsonText)
      // throw on anything the schema doesn't allow, instead of quietly emptying the editor
      editor.commands.setContent(json, { errorOnInvalidContent: true })
      error = ''
    } catch (err) {
      // Tiptap puts the real reason (e.g. "Unknown node type: script") in err.cause
      error = String(err instanceof Error && err.cause ? err.cause : err)
    }
  }
</script>

<main>
  <div class="editor" bind:this={element}></div>

  <button onclick={getJSON}>Get JSON</button>
  <button onclick={loadJSON}>Load JSON</button>

  {#if error}
    <p class="error">{error}</p>
  {/if}

  <textarea bind:value={jsonText} rows="16" spellcheck="false"></textarea>
</main>

<style>
  main {
    padding: 1.5rem;
  }

  .editor {
    border: 2px solid var(--gray-3);
    border-radius: 0.75rem;
  }

  .editor:focus-within {
    border-color: var(--purple);
  }

  button {
    margin: 1rem 0.5rem 1rem 0;
  }

  textarea {
    display: block;
    width: 100%;
    font-family: monospace;
    border: 2px solid var(--gray-3);
    border-radius: 0.75rem;
    padding: 1rem;
  }

  .error {
    color: crimson;
  }
</style>
