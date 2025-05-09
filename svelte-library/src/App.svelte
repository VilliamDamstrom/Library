<script>
  import Library from './components/Library.svelte';
</script>

<main>
  <h1>My Library</h1>
  <Library />
</main>

<style>
  main {
    max-width: 800px;
    margin: 0 auto;
    padding: 1rem;
    font-family: sans-serif;
  }

  h1 {
    text-align: center;
    margin-bottom: 2rem;
  }
</style>