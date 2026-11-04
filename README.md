# sv

Everything you need to build a Svelte project, powered by [`sv`](https://github.com/sveltejs/cli).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```sh
# create a new project
npx sv create my-app
```

To recreate this project with the same configuration:

```sh
# recreate this project
npx sv@1.1.1 create --template minimal --types jsdoc --add prettier eslint --install npm .
```

## Adding features

Add features to your project with `sv add`:

```sh
npx sv add
```

For example, to add Tailwind CSS:

```sh
npx sv add tailwindcss
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```sh
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```sh
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.


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