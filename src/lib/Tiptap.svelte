<script>
  import { onMount, onDestroy } from 'svelte'
  import { Editor } from '@tiptap/core'
  import { StarterKit } from '@tiptap/starter-kit'
  import BubbleMenu from '@tiptap/extension-bubble-menu'

  let bubbleMenu = $state()
  let element = $state()
  /** @type {{ editor: Editor | null }} */
  let editorState = $state({editor: null})

  onMount(() => {
    editorState.editor = new Editor({
      element: element,
      extensions: [
        StarterKit,
        BubbleMenu.configure({
          element: bubbleMenu,
        }),
      ],
      content: `
        <h1>Hello Svelte! 🐼 </h1>
        <p>This editor is running in Svelte.</p>
        <p>Select some text to see the bubble menu popping up.</p>
      `,
      onTransaction: ({ editor }) => {
        // Update the state signal to force a re-render
        editorState = { editor }
      },
    })
  })
  onDestroy(() => {
    editorState.editor?.destroy()
  })

  // JSON text shown in / read from the textarea below the editor
  let jsonText = $state('')
  let loadError = $state('')

  // Read the document as JSON (this is what we will save, never HTML)
  function getJSON() {
    if (!editorState.editor) return
    jsonText = JSON.stringify(editorState.editor.getJSON(), null, 2)
    loadError = ''
  }

  // Restore a saved JSON document into the editor
  function loadJSON() {
    if (!editorState.editor) return
    try {
      const doc = JSON.parse(jsonText)
      // errorOnInvalidContent makes Tiptap reject anything that doesn't fit the editor's schema instead of loading part of it
      editorState.editor.commands.setContent(doc, { errorOnInvalidContent: true }) 
      editorState.editor.commands.focus()
      loadError = ''
    } catch (err) {
      loadError = err instanceof Error ? err.message : String(err)
    }
  }
</script>

<div style="position: relative" class="app">
  {#if editorState.editor}
    <div class="fixed-menu">
      <button
        onclick={() => editorState.editor?.chain().focus().toggleHeading({ level: 1 }).run()}
        class:active={editorState.editor.isActive('heading', { level: 1 })}
      >
        H1
      </button>
      <button
        onclick={() => editorState.editor?.chain().focus().toggleHeading({ level: 2 }).run()}
        class:active={editorState.editor.isActive('heading', { level: 2 })}
      >
        H2
      </button>
      <button onclick={() => editorState.editor?.chain().focus().setParagraph().run()} class:active={editorState.editor.isActive('paragraph')}>
        P
      </button>

      <!-- New addition -->
      <button onclick={() => editorState.editor?.chain().focus().toggleItalic().run()} class:active={editorState.editor.isActive('italic')}>
      I
      </button>

    </div>
  {/if}

  <div bind:this={element}></div>

  <div class="json-panel">
    <button onclick={getJSON}>Get JSON</button>
    <button onclick={loadJSON}>Load JSON</button>
    {#if loadError}
      <p class="error">Could not load: {loadError}</p>
    {/if}
    <textarea bind:value={jsonText} rows="12" placeholder="Click Get JSON, edit or paste JSON here, then Load JSON"></textarea>
  </div>
</div>

<style>
  .json-panel textarea {
    display: block;
    width: 100%;
    font-family: monospace;
  }
  .error {
    color: crimson;
  }
  button.active {
    background: black;
    color: white;
  }
</style>
