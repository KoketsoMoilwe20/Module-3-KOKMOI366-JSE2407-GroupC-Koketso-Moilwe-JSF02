<script>
    import {Router, Link, Route} from "svelte-routing"
    import Header from "./Components/Header.svelte";
    import ProductList from "./Components/Products/ProductList.svelte";
    import {selectedCategory, searchQuery, sortOption} from "./Components/ProductStore/store";
    import {onMount} from "svelte";

    
</script>

<style>
    
</style>

<Router>
    <Header />
</Router>
