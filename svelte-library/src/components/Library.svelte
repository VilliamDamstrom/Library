<script>
  import { onMount } from 'svelte';
  import Book from './Book.svelte';
  import Album from './Album.svelte';
  import Movie from './Movie.svelte';
  import AddItemForm from './AddItemForm.svelte';

  let items = [];

  onMount(async () => {
    try {
      const res = await fetch('http://localhost:3000/items');
      if (!res.ok) throw new Error('Failed to fetch items');
      items = await res.json();
      console.log('Fetched items:', items); // Debugging
    } catch (error) {
      console.error('Error fetching items:', error);
    }
  });

  async function addItem(newItem) {
    try {
      const res = await fetch('http://localhost:3000/items', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(newItem),
      });
      if (!res.ok) throw new Error('Failed to add item');
      const addedItem = await res.json();
      items = [...items, addedItem];
      console.log('Updated items:', items); // Debugging
    } catch (error) {
      console.error('Error adding item:', error);
    }
  }

  function getComponent(type) {
    if (type === 'Book') return Book;
    if (type === 'Album') return Album;
    if (type === 'Movie') return Movie;
    console.warn(`Unknown type: ${type}`);
    return null;
  }
</script>

<!-- My Library Section -->
<h2>My Library</h2>
<div class="library-list">
  {#if items.length > 0}
    {#each items as item (item.id)}
      {#if getComponent(item.type)}
        <svelte:component this={getComponent(item.type)} {item} />
      {:else}
        <p>Unknown item type: {item.type}</p>
      {/if}
    {/each}
  {:else}
    <p>No items found. Add a new item to your library!</p>
  {/if}
</div>

<!-- Add Item Form Section -->
<AddItemForm on:add={e => addItem(e.detail)} />

<style>
  .library-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 1rem;
    margin-bottom: 2rem;
  }
</style>