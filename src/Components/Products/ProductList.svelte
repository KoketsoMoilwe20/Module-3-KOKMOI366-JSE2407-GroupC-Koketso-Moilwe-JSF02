<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';
    import {Link} from "svelte-routing"
    import { selectedCategory, searchQuery, sortOption } from '../store';

    import Sort from '../Sort.svelte';
  
    const products = writable([]);
    let isLoading = true;
    
    onMount(async () => {
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
    });
  
    $: filteredProducts = $products.filter(product => {
      return (!$selectedCategory || product.category === $selectedCategory) &&
             (!$searchQuery || product.title.toLowerCase().includes($searchQuery.toLowerCase()));
    });
  
    $: sortedProducts = sortProducts(filteredProducts, $sortOption);
  
    $: categories = [...new Set($products.map(product => product.category))];
  
    function handleCategoryChange(event) {
      selectedCategory.set(event.target.value);
    }
  
    function handleSearchChange(event) {
      searchQuery.set(event.target.value);
    }
  
    function handleSort(option) {
      sortOption.set(option);
    }
  
    function sortProducts(products, option) {
      let sortedProducts = [...products];
      switch (option) {
        case 'low-to-high':
          return sortedProducts.sort((a, b) => a.price - b.price);
        case 'high-to-low':
          return sortedProducts.sort((a, b) => b.price - a.price);
        default:
          return sortedProducts;
      }
    }
  </script>
  
  <style>

  </style>
  
  <div class="filters-and-sort">
    <div class="filters">
      <select bind:value={$selectedCategory} on:change={handleCategoryChange}>
        <option value="">All categories</option>
        {#each categories as category}
          <option value={category}>{category}</option>
        {/each}
      </select>
      <input 
        type="text" 
        placeholder="Search products..." 
        bind:value={$searchQuery}
        on:input={handleSearchChange}
      />
    </div>
    <Sort onSort={handleSort} currentSort={$sortOption} />
  </div>
  
  {#if isLoading}
    <div class="loading-spinner">
      <div class="spinner"></div>
    </div>
  {:else}
    <div class="product-grid">
      {#each sortedProducts as product (product.id)}
        <Link to={`/product/${product.id}`} class="product-card">
          <img src={product.image} alt={product.title} />
          <h2>{product.title}</h2>
          <p>${product.price.toFixed(2)}</p>
          <p>{product.category}</p>
          <p>{product.rating.rate} ★ ({product.rating.count} reviews)</p>
          <button>Add to Cart</button>
        </Link>
      {:else}
        <p>No products found.</p>
      {/each}
    </div>
  {/if}