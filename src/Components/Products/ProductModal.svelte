<script>
    import { onMount } from 'svelte';
    import { Link } from "svelte-routing";

    import { selectedCategory, searchQuery, sortOption } from "../store"

    export let id;
    let product = null;
    let isLoading = true;

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