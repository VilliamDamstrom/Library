<!-- src/App.svelte -->
<script>
  import Library from './components/Library.svelte';
</script>

<main>
  <h1>My Favorite Books</h1>
  <Library />
</main>

<style>
main {
  max-width: 800px;
  margin: 0 auto;
  padding: 1rem;
  font-family: sans-serif;
}
</style>