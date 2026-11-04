<script>
  import '#lib/style.css'
  import { onMount } from 'svelte'
  import { Editor, generateHTML } from '@tiptap/core'
  import StarterKit from '@tiptap/starter-kit'

  // will point at the <div> below once the page loads
  let element = $state()
  // not $state because nothing on the page needs to update when this changes
  let editor
  // we need a variable to hold the saved HTML
  let savedHTML =  $state()

  // the editor needs a real element to attach to, and that only exists
  // after the component has loaded, so we create it inside onMount
  onMount(() => {
    editor = new Editor({
      element,
      // StarterKit is a bundle of the basics: bold, italic, headings, lists, undo
      extensions: [StarterKit],
      // just a pre-defined content, feel free to make it empty instead
      content: '<p>Hello World!</p>',
    })

    // cleanup: runs when the component is removed from the page
    return () => editor.destroy()
  })

  function save() {
    // the editor's content as JSON, which is what we normally store
    const json = editor.getJSON()
    // turn that JSON into an HTML string. It needs StarterKit again so it
    // knows how to write things like bold text and headings as HTML
    savedHTML = generateHTML(json, [StarterKit])
  }

</script>

<main>
  <!-- Tiptap builds the editable area inside this div -->
  <div class="editor" bind:this={element}></div>

   <button onclick={save}>Save</button>

   <!-- hidden until Save has been clicked -->
   {#if savedHTML}
     <!-- {@html} shows the string as real HTML instead of printing the tags as text.
          That's only safe here because the HTML came from our own editor. Don't use
          it on HTML from users or other sources without cleaning it first. -->
     <!-- eslint-disable-next-line svelte/no-at-html-tags -->
     <article>{@html savedHTML}</article>
    {/if}
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
        margin: 1rem 0;
    }

    article {
        background: var(--gray-1);
        border-radius: 0.75rem;
        padding: 1rem 1.5rem;
    }
</style>