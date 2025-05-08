<script>
  import { writable } from 'svelte/store';

  let count = writable(0);
  const increment = () => {
    count.update(n => n + 1);
  };
</script>

<button on:click={increment}>
  count is {$count}
</button>