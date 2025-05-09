<script>
  import { onMount } from 'svelte';
  import AddItemForm from './AddItemForm.svelte';

  let items = [];

  // Fetch items from the backend on component mount
  onMount(async () => {
    try {
      const res = await fetch('http://localhost:3000/items');
      if (!res.ok) throw new Error('Failed to fetch items');
      items = await res.json();
    } catch (error) {
      console.error('Error fetching items:', error);
    }
  });

  // Add a new item to the library
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
    } catch (error) {
      console.error('Error adding item:', error);
    }
  }
</script>

<!-- My Library Section -->
<h2>My Library</h2>
<div class="library-list">
  {#if items.length > 0}
    {#each items as item (item.id)}
      <div class="item-card">
        <img src={item.image} alt={item.title || 'Item cover'} />
        <div class="item-info">
          <h3>{item.title}</h3>
          {#if item.author}
            <p><strong>Author:</strong> {item.author}</p>
          {:else if item.artist}
            <p><strong>Artist:</strong> {item.artist}</p>
          {:else if item.director}
            <p><strong>Director:</strong> {item.director}</p>
          {/if}
          <p><strong>Year:</strong> {item.year || 'N/A'}</p>
        </div>
      </div>
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

  .item-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 1rem;
    background-color: #fdfdfd;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
  }

  .item-card img {
    max-width: 100%;
    height: auto;
    margin-bottom: 0.5rem;
    border-radius: 4px;
  }

  .item-info {
    color: black !important; /* Ensure text is visible */
    font-size: 16px !important; /* Ensure text is readable */
  }

  .item-info p, .item-info h3 {
    display: block !important; /* Ensure elements are not hidden */
  }
</style>