<script>

    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';

    import {selectedCategory, searchQuery, sortOption} from "../ProductStore/store"

    function handleCategoryChange(event) {
      selectedCategory.set(event.target.value);
    }
</script>

<style>

</style>

<div class="filters-and-sort">

    <div class="filters">

    </div>

</div>