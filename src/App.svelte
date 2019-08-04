<script>
  import Product from "./Product.svelte";
  import Cart from "./Cart.svelte";
  import Button from "./Button.svelte";

  let title = "";
  let price = 0;
  let description = "";

  let products = [];
  let cartItems = [];

  function setTitle(event) {
    title = event.target.value;
  }

  function createProduct() {
    const newProduct = {
      title: title,
      price: price,
      description: description
    };
    //to change the reference, to indicate change so that DOM will be rerendered.
    products = products.concat(newProduct);
  }

  //custom event
  function addToCart(event) {
    const title = event.detail;
    console.log(title);
    cartItems = cartItems.concat({
      ...products.find(prod => prod.title == title)
    });
    console.log(cartItems); 
  }
</script>

<style>
  h1 {
    color: purple;
  }
  section {
    width: 30rem;
    margin: auto;
  }

  textarea,
  label,
  input {
    width: 100%;
  }
</style>

<section>
  <Cart items={cartItems} />
</section>

<section>
  <div>
    <label for="title">Title</label>
    <input id="title" value={title} on:input={setTitle} />
  </div>
  <div>
    <label for="price">Price</label>
    <input type="number" id="price" bind:value={price} />
  </div>
  <div>
    <label for="description">Description</label>
    <textarea rows="3" id="description" bind:value={description} />
  </div>
  <Button on:click={createProduct}>Create Product</Button>
</section>

{#if products.length === 0}
  <p>No products were added yet.</p>
{:else}
  {#each products as oneProduct}
    <Product
      productTitle={title}
      productPrice={price}
      productDescription={description}
      on:addcart={addToCart} />
  {/each}
{/if}
