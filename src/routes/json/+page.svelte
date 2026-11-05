<script>
  import '#lib/style.css'
  import { onMount } from 'svelte'
  import { Editor } from '@tiptap/core'
  import StarterKit from '@tiptap/starter-kit'

  let element = $state()
  /** @type {Editor} */
  let editor
  
  // Todo 1
  let jsonText = $state('')

  onMount(() => {
    editor = new Editor({
      element,
      extensions: [StarterKit],
      content: '<h2>My note</h2><p>This is <em>italic</em> and this is <strong>bold</strong>.</p>',
    })

    return () => editor.destroy()
  })

  // TODO 2: getJSON()

  // TODO 4: loadJSON()
</script>


<main>
  <div class="editor" bind:this={element}></div>

  <!-- TODO 3: Get JSON button + textarea -->

  <textarea bind:value={jsonText} rows="16" spellcheck="false"></textarea>

  <!-- TODO 5: Load JSON button -->
</main>

<style>
  main {
    padding: 1.5rem;
  }

  .editor {
    border: 2px solid var(--gray-3);
    border-radius: 0.75rem;
  }

  textarea {
    display: block;
    width: 100%;
    font-family: monospace;
  }
</style>