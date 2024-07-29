<script>

    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';

    import {selectedCategory, searchQuery, sortOption} from "../ProductStore/store"

    const products = writable([]);
    let isLoading = true;

    onMount (async () => {
        try {
        const res = await fetch('https://fakestoreapi.com/products');
        if (!res.ok) throw new Error('Failed to fetch products');
        const data = await res.json();
        products.set(data);
      } catch (error) {
        console.error('Error fetching products:', error);
        products.set([]);
      } finally {
        isLoading = false;
      }
    })

    function handleCategoryChange(event) {
      selectedCategory.set(event.target.value);
    }
</script>



<style>

</style>



{#if isLoading}
    <p>Loading products...</p>
{:else}
    <div class="product-grid">
      {#each $products as product (product.id)}
        <div class="product-card">
          <h2>{product.title}</h2>
          <p>${product.price.toFixed(2)}</p>
        </div>
      {:else}
        <p>No products found.</p>
      {/each}
    </div>
{/if}