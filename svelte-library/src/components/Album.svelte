<script>
  export let item;
</script>

<div class="media-card">
  <img src={item.image} alt={item.title || 'Album cover'} />
  <h3>{item.title}</h3>
  <p><strong>{item.artist}</strong></p>
  <p>{item.year}</p>
</div>

<style>
  .media-card {
    border: 1px solid #ccc;
    padding: 1rem;
    border-radius: 8px;
    text-align: center;
    background-color: #fdfdfd;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
  }

  img {
    max-width: 100%;
    height: auto;
    margin-bottom: 0.5rem;
  }

  h3 {
    margin: 0.5rem 0 0.2rem;
  }

  p {
    margin: 0.2rem 0;
  }
</style>