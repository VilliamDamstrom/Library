<!-- src/components/Library.svelte -->
<script>
  import { onMount } from 'svelte';
  import Book from './Book.svelte';

  let items = [];

  onMount(async () => {
    const res = await fetch('http://localhost:3000/items'); // matches your db.json
    items = await res.json();
  });
</script>

<h2>Your Library</h2>

{#if items.length > 0}
  <div class="library-list">
    {#each items as item}
      <Book {item} />
    {/each}
  </div>
{:else}
  <p>Loading or no items found...</p>
{/if}

<style>
.library-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  gap: 1rem;
}
</style>