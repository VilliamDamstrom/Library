<!-- src/components/Book.svelte -->
<script>
  export let item;
</script>

<div class="book-card">
  <img src={item.image} alt={item.title} />
  <h3>{item.title}</h3>
  <p>{item.author}</p>
  <p>{item.year}</p>
</div>

<style>
.book-card {
  border: 1px solid #ccc;
  padding: 1rem;
  border-radius: 8px;
  text-align: center;
}
img {
  max-width: 100%;
  height: auto;
}
</style>