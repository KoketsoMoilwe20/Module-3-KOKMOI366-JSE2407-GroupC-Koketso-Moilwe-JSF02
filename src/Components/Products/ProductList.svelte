<script>
  import { onMount } from 'svelte';
  import { writable } from 'svelte/store';
  import { Link } from 'svelte-routing';
  import { selectedCategory, searchQuery, sortOption } from '../ProductStore/store';
  import Sort from '../Sort.svelte';

// Created a writable store to hold the products data
  const products = writable([]);
  let isLoading = true;

  // Fetch the products data from the API when the component mounts
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

  // Reactive statement to filter products based on selected category and search query
  $: filteredProducts = $products.filter(product => {
    return (!$selectedCategory || product.category === $selectedCategory) &&
           (!$searchQuery || product.title.toLowerCase().includes($searchQuery.toLowerCase()));
  });

  // Reactive statement to sort the filtered products based on the selected  sort option
  $: sortedProducts = sortProducts(filteredProducts, $sortOption);

  // Reactive statement to get a unique list of categories from the products
  $: categories = [...new Set($products.map(product => product.category))];

  //Handle category selection change
  function handleCategoryChange(event) {
    selectedCategory.set(event.target.value);
  }

    // Handle search query input change
  function handleSearchChange(event) {
    searchQuery.set(event.target.value);
  }

  //Handle sorting option change
  function handleSort(option) {
    sortOption.set(option);
  }

  //Function to sort products based on the selected sorting option
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

    button {
        background-color: #F7B318;
    }

    button:hover {
        background-color: #F39C12;
    }

    


  .spinner {
    border: 4px solid rgba(0, 0, 0, 0.1);
    border-top: 4px solid #3490dc;
    border-radius: 50%;
    width: 24px;
    height: 24px;
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }
</style>

<div class="filters-and-sort mb-8">
    <div class="flex items-center justify-center space-x-4 mb-4">
      <select bind:value={$selectedCategory} on:change={handleCategoryChange} class="bg-white border border-gray-300 rounded-md px-4 py-2">
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
        class="bg-white border border-gray-300 rounded-md px-4 py-2"
      />
    </div>
    <Sort onSort={handleSort} />
  </div>
  
  {#if isLoading}
    <div class="flex justify-center items-center h-64">
      <div class="spinner"></div>
    </div>
  {:else}
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      {#each sortedProducts as product (product.id)}
        <Link to={`/product/${product.id}`} class="product-card bg-white border border-gray-200 rounded-lg shadow-md overflow-hidden">
          <img src={product.image} alt={product.title} class="object-contain h-48 mt-3"/>
          <div class="p-4">
            <h2 class="text-lg font-semibold mb-2">{product.title}</h2>
            <p class="text-gray-700 mb-2">${product.price.toFixed(2)}</p>
            <p class="text-gray-500 mb-2">{product.category}</p>
            <p class="text-gray-500 mb-4">{product.rating.rate} ★ ({product.rating.count} reviews)</p>
            <button class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">Add to Cart</button>
          </div>
        </Link>
      {:else}
        <p class="text-center col-span-full">No products found.</p>
      {/each}
    </div>
  {/if}