<script>
  export let items;

  $: cartTotal = items.reduce((sum, currentValue) => {
    return sum + currentValue.price;
  }, 0);
</script>

<style>
  ul {
    list-style: none;
    margin: 1rem;
    padding: 0;
  }
  li {
    margin: 0.5rem 0;
    padding: 0.5rem;
    border: 1px solid #ccc;
  }
  h1 {
    font-size: 1.5rem;
    margin: 1rem;
  }
</style>

<ul>
  {#if items.length === 0}
    <p>No items added to cart yet.</p>
  {:else}
    {#each items as item}
      <li>{item.title} - ${item.price}</li>
    {/each}
  {/if}
</ul>

<h1>TOTAL : ${cartTotal}</h1>
