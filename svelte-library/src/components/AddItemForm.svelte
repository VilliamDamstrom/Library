<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  let title = '';
  let creator = ''; // Could be author, artist, or director
  let year = '';
  let image = '';
  let type = 'Book';

  function handleSubmit(e) {
    e.preventDefault();

    const newItem = {
      title,
      image,
      type,
      borrowed: false,
    };

    // Assign correct property name based on type
    if (type === 'Book') newItem.author = creator;
    if (type === 'Album') newItem.artist = creator;
    if (type === 'Movie') newItem.director = creator;

    console.log('New item:', newItem); // Debugging
    dispatch('add', newItem);

    // Reset form
    title = '';
    creator = '';
    year = '';
    image = '';
    type = 'Book';
  }
</script>

<form on:submit={handleSubmit}>
  <h3>Add a New Item</h3>

  <label>Type:</label>
  <select bind:value={type}>
    <option>Book</option>
    <option>Album</option>
    <option>Movie</option>
  </select>

  <label>Title:</label>
  <input bind:value={title} required />

  <label>{type === 'Book' ? 'Author' : type === 'Album' ? 'Artist' : 'Director'}:</label>
  <input bind:value={creator} required />

  <label>Image URL:</label>
  <input bind:value={image} required />

  <button type="submit">Add Item</button>
</form>

<style>
  form {
    margin-bottom: 2rem;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  input, select {
    padding: 0.4rem;
    font-size: 1rem;
  }

  button {
    margin-top: 0.5rem;
    padding: 0.6rem;
    background-color: #2c7;
    border: none;
    color: white;
    font-weight: bold;
    cursor: pointer;
  }

  button:hover {
    background-color: #1a5;
  }
</style>