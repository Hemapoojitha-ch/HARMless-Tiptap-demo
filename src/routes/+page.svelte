<!-- <script>
  let note = $state('');
</script>

<h1>First Svelte Page</h1>

<h2>My notes</h2>

<textarea
  bind:value={note}
  placeholder="Write your note here..."
></textarea>

<h3>Live Preview</h3>

<p>{note || 'Your note will appear here'}</p> -->

<!-- This is the sample code from the svelte tutorial -->
<script>
  import Tiptap from '$lib/Tiptap.svelte'
</script>

<main>
  <Tiptap />
</main>