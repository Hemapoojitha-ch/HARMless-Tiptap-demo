<script>
  import '#lib/style.css'
  import { onMount } from 'svelte'
  // TODO 1: import generateHTML
  import { Editor } from '@tiptap/core'
  import StarterKit from '@tiptap/starter-kit'

  let element = $state()
  let editor
  // TODO 2: a variable to hold the saved HTML

  onMount(() => {
    editor = new Editor({
      element,
      extensions: [StarterKit],
      content: '<p>Hello World!</p>',
    })

    return () => editor.destroy()
  })

  // TODO 3: the save function (editor > JSON > HTML)

</script>

<main>
  <div class="editor" bind:this={element}></div>

  <!-- TODO 4: a Save button -->

  <!-- TODO 5: show the saved post (only after Save has been clicked) -->
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

  /* TODO 6 (optional): style the Save button and the saved post */
</style>