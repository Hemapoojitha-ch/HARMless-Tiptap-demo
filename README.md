# HARMless Tiptap Demo

Tiptap Tech share!. Tiptap is a rich-text editor, we provided a basic examples of using it, also a page for loading and saving editor JSON, and a starter page for turning editor content into HTML.

## What's here

- **`/` - Editor:**  [src/lib/Tiptap.svelte](./src/lib/Tiptap.svelte). Shows that with Tiptap, it supports bold, italic, strike-through, inline code, paragraphs, H1–H3 headings, bullet and numbered lists, code blocks, blockquotes, horizontal rules, hard breaks, undo, and redo. **Save** shows an HTML preview, **Edit** takes you back to the editor.
- **`/json` - JSON:** **Get JSON** copies the current document into the text area. You can also edit or paste JSON there and choose **Load JSON** to update the editor. The page shows an error if the JSON is invalid or doesn't fit the editor's schema.
- **`/render`- Render:** This page is specifically for saving editor content as HTML.

## Run the app

Install the dependencies and start the dev server:

```sh
npm install
npm run dev
```

Vite prints the local address in the terminal. To build and preview the production version:

```sh
npm run build
npm run preview
```

You can run `npm run check` for Svelte and type checks, or `npm run lint` for formatting and lint checks.

If you're adding Tiptap to your existing project, you can proceed to Install Tiptap editor and starter kit by running this command:

```sh
npm install @tiptap/core @tiptap/starter-kit
```

StarterKit includes common formatting and document types, such as paragraphs, headings, lists, bold, and italic. Install other Tiptap extensions for features you need that StarterKit doesn't include.

## Other Resources

- [Tiptap: install guide for Svelte](https://tiptap.dev/docs/editor/getting-started/install/svelte)
- [Tiptap: Default text editor example](https://tiptap.dev/docs/examples/basics/default-text-editor)
- [Tiptap: Minimal setup example](https://tiptap.dev/docs/examples/basics/minimal-setup)
- [Tiptap: saving and showing content (JSON and HTML)](https://tiptap.dev/docs/guides/output-json-html)
- [Tiptap: generateHTML](https://tiptap.dev/docs/editor/api/utilities/html)
- [Tiptap source code and demos on GitHub](https://github.com/ueberdosis/tiptap)
- [Tiptap: what's free and what's paid](https://tiptap.dev/pricing)
- [Svelte: the {@html} tag](https://svelte.dev/docs/svelte/@html)
- [Svelte: interactive tutorial](https://svelte.dev/tutorial)
- [Svelte: creating a project with sv create](https://svelte.dev/docs/cli/sv-create)
