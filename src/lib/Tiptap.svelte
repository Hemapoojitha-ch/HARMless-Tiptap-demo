<script>
  import "./styles.css";
  import "./style.css";

  import { Color } from '@tiptap/extension-text-style'
  import { ListItem, TaskItem, TaskList } from '@tiptap/extension-list'
  import { TextStyle } from '@tiptap/extension-text-style'
  import StarterKit from "@tiptap/starter-kit";
  import { Editor, generateHTML } from "@tiptap/core";
  import { onMount } from "svelte";

  // oxlint-disable-next-line
  let element = $state();
  let editorState = $state({ editor: null });
  let savedHTML = $state();
  let isEditing = $state(true);

  function save() {
    const json = editorState.editor.getJSON();
    savedHTML = generateHTML(json, extensions);
    isEditing = false;
  }

  function edit() {
    isEditing = true;
  }

  const extensions = [
    Color.configure({ types: [TextStyle.name, ListItem.name] }),
    TextStyle.configure({ types: [ListItem.name] }),
    StarterKit,
    TaskItem.configure({ nested: true }),
    TaskList,
  ];

  onMount(() => {
    editorState.editor = new Editor({
      element: element,
      extensions,
      content: `
            <h2>
              Hi there,
            </h2>
            <p>
              this is a <em>basic</em> example of <strong>Tiptap</strong>. Sure, there are all kind of basic text styles you’d probably expect from a text editor. But wait until you see the lists:
            </p>
            <ul>
              <li>
                That’s a bullet list with one …
              </li>
              <li>
                … or two list items.
              </li>
            </ul>
            <p>
              Isn’t that great? And all of that is editable. But wait, there’s more. Let’s try a code block:
            </p>
            <pre><code class="language-css">body {
  display: none;
}</code></pre>
            <p>
              I know, I know, this is impressive. It’s only the tip of the iceberg though. Give it a try and click a little bit around. Don’t forget to check the other examples too.
            </p>
            <blockquote>
              Wow, that’s amazing. Good work, boy! 👏
              <br />
              — Mom
            </blockquote>
          `,
      onTransaction: ({ editor }) => {
        // force re-render so `editor.isActive` works as expected
        // oxlint-disable-next-line no-self-assign
        editorState = { editor };
      },
    });
    return () => {
      editorState.editor?.destroy();
    };
  });
</script>

<div hidden={!isEditing}>
{#if editorState.editor}
  <div class="control-group">
    <div class="button-group">
      <button
        onclick={() => editorState.editor.chain().focus().toggleBold().run()}
        disabled={!editorState.editor.can().chain().focus().toggleBold().run()}
        class={editorState.editor.isActive("bold") ? "is-active" : ""}
      >
        Bold
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleItalic().run()}
        disabled={!editorState.editor.can().chain().focus().toggleItalic().run()}
        class={editorState.editor.isActive("italic") ? "is-active" : ""}
      >
        Italic
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleStrike().run()}
        disabled={!editorState.editor.can().chain().focus().toggleStrike().run()}
        class={editorState.editor.isActive("strike") ? "is-active" : ""}
      >
        Strike
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleCode().run()}
        disabled={!editorState.editor.can().chain().focus().toggleCode().run()}
        class={editorState.editor.isActive("code") ? "is-active" : ""}
      >
        Code
      </button>
      <button onclick={() => editorState.editor.chain().focus().unsetAllMarks().run()}>Clear marks</button>
      <button onclick={() => editorState.editor.chain().focus().clearNodes().run()}>Clear nodes</button>
      <button
        onclick={() => editorState.editor.chain().focus().setParagraph().run()}
        class={editorState.editor.isActive("paragraph") ? "is-active" : ""}
      >
        Paragraph
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleHeading({ level: 1 }).run()}
        class={editorState.editor.isActive("heading", { level: 1 }) ? "is-active" : ""}
      >
        H1
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleHeading({ level: 2 }).run()}
        class={editorState.editor.isActive("heading", { level: 2 }) ? "is-active" : ""}
      >
        H2
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleHeading({ level: 3 }).run()}
        class={editorState.editor.isActive("heading", { level: 3 }) ? "is-active" : ""}
      >
        H3
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleHeading({ level: 4 }).run()}
        class={editorState.editor.isActive("heading", { level: 4 }) ? "is-active" : ""}
      >
        H4
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleHeading({ level: 5 }).run()}
        class={editorState.editor.isActive("heading", { level: 5 }) ? "is-active" : ""}
      >
        H5
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleHeading({ level: 6 }).run()}
        class={editorState.editor.isActive("heading", { level: 6 }) ? "is-active" : ""}
      >
        H6
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleBulletList().run()}
        class={editorState.editor.isActive("bulletList") ? "is-active" : ""}
      >
        Bullet list
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleOrderedList().run()}
        class={editorState.editor.isActive("orderedList") ? "is-active" : ""}
      >
        Ordered list
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleTaskList().run()}
        class={editorState.editor.isActive("taskList") ? "is-active" : ""}
      >
        Task list
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleCodeBlock().run()}
        class={editorState.editor.isActive("codeBlock") ? "is-active" : ""}
      >
        Code block
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().toggleBlockquote().run()}
        class={editorState.editor.isActive("blockquote") ? "is-active" : ""}
      >
        Blockquote
      </button>
      <button onclick={() => editorState.editor.chain().focus().setHorizontalRule().run()}>
        Horizontal rule
      </button>
      <button onclick={() => editorState.editor.chain().focus().setHardBreak().run()}>Hard break</button>
      <button
        onclick={() => editorState.editor.chain().focus().undo().run()}
        disabled={!editorState.editor.can().chain().focus().undo().run()}
      >
        Undo
      </button>
      <button
        onclick={() => editorState.editor.chain().focus().redo().run()}
        disabled={!editorState.editor.can().chain().focus().redo().run()}
      >
        Redo
      </button>
      <button
        onclick={() =>  {
            if (editorState.editor.isActive('textStyle', { color: 'purple' })) {
                editorState.editor.chain().focus().unsetColor().run();
            } else {
            editorState.editor.chain().focus().setColor('purple').run();
            }
        }}
        class={editorState.editor.isActive('textStyle', { color: 'purple' }) ? 'is-active' : ''}
      >
        Purple
      </button>

    </div>
  </div>
{/if}

<div class="editor" bind:this={element}></div>
<div class="control-group">
  <div class="button-group">
    <button onclick={save}>Save</button>
  </div>
</div>
</div>

{#if !isEditing}
    <!-- eslint-disable-next-line svelte/no-at-html-tags -->
    <article class="tiptap">{@html savedHTML}</article>
    <div class="control-group">
      <div class="button-group">
        <button onclick={edit}>Edit</button>
      </div>
    </div>
  {/if}

<style>
  .editor {
    margin: 20px;
    border: 2px solid var(--gray-3);
    border-radius: 0.75rem;
  }

  .editor:focus-within {
    border-color: var(--purple);
  }
</style>