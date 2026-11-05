<script>
  import '#lib/style.css'
  import { onMount } from 'svelte'
  import { Editor } from '@tiptap/core'
  import StarterKit from '@tiptap/starter-kit'

  let element = $state()
  /** @type {Editor} */
  let editor
  
  // Reactive variable
  let jsonText = $state('')

  onMount(() => {
    editor = new Editor({
      element,
      extensions: [StarterKit],
      content: '<h2>My note</h2><p>This is <em>italic</em> and this is <strong>bold</strong>.</p>',
    })

    return () => editor.destroy()
  })

  // TODO 1: getJSON()
  function getJSON(){}

  // TODO 2: loadJSON()
  function loadJSON(){}

</script>


<main>
  <div class="editor" bind:this={element}></div>

  <!-- Get JSON button -->
  <button onclick={getJSON}>Get JSON</button>

  <!-- Load JSON button -->
  <button onclick={loadJSON}>Load JSON</button>

  <!-- textarea connected to jsonText -->
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

  button {
    margin: 1rem 0.5rem 1rem 0;
  }

  textarea {
    display: block;
    width: 100%;
    font-family: monospace;
  }
</style>