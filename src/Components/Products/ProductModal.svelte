<script>
    import { onMount } from 'svelte';
    import { Link } from "svelte-routing";

    import { selectedCategory, searchQuery, sortOption } from "../ProductStore/store"

    export let id;
    let product = null;
    let isLoading = true;


    // Fetch the product data from the API when the component mounts
    onMount(async () => {
      try {
        const res = await fetch(`https://fakestoreapi.com/products/${id}`);
        if (!res.ok) throw new Error('Failed to fetch product');
        product = await res.json();
      } catch (error) {
        console.error('Error fetching product:', error);
      } finally {
        isLoading = false;
      }
    });
  
    $: backUrl = `/?category=${$selectedCategory}&search=${$searchQuery}&sort=${$sortOption}`;
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

{#if isLoading}
    <div class="flex justify-center items-center h-screen">
      <div class="spinner"></div>
    </div>
  {:else if product}
    <div class="modal-content flex bg-white rounded-lg shadow-lg overflow-hidden max-w-4xl mx-auto p-6">
      <div class="flex-shrink-0 w-1/2">
        <img src={product.image} alt={product.title} class="w-full h-full object-cover rounded-lg" />
      </div>
      <div class="flex-grow pl-6">
        <h2 class="text-2xl font-bold mb-4">{product.title}</h2>
        <p class="text-lg font-semibold mb-2"><strong>Price:</strong> ${product.price.toFixed(2)}</p>
        <p class="text-lg font-semibold mb-2"><strong>Category:</strong> {product.category}</p>
        <p class="text-lg font-semibold mb-2"><strong>Rating:</strong> {product.rating.rate} ★ ({product.rating.count} reviews)</p>
        <p class="text-lg mb-4"><strong>Description:</strong> {product.description}</p>
        <button class="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-blue-600 transition">Add to Cart</button>
        <Link to={backUrl} class="block mt-4 text-blue-500 hover:underline">Back to Results</Link>
      </div>
    </div>
  {:else}
    <p class="text-center">Error loading product. Please try again.</p>
  {/if}