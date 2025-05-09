<script>
  import { onMount } from 'svelte';
  import Book from './Book.svelte';
  import Album from './Album.svelte';
  import Movie from './Movie.svelte';

  let items = [];

  onMount(async () => {
    const res = await fetch('http://localhost:3000/items');
    items = await res.json();
  });
</script>

<h2>Your Library</h2>

{#if items.length > 0}
  <div class="library-list">
    {#each items as item}
      {#if item.type === 'book'}
        <Book {item} />
      {:else if item.type === 'album'}
        <Album {item} />
      {:else if item.type === 'movie'}
        <Movie {item} />
      {:else}
        <p>Unknown item type: {item.type}</p>
      {/if}
    {/each}
  </div>
{:else}
  <p>Loading or no items found...</p>
{/if}

<style>
  h2 {
    margin-bottom: 1rem;
  }

  .library-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 1rem;
  }
</style>