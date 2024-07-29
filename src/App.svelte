<script>
    import {Router, Link, Route} from "svelte-routing"
    import Header from "./Components/Header.svelte";
    import ProductList from "./Components/Products/ProductList.svelte";
    import {selectedCategory, searchQuery, sortOption} from "./Components/store";
    import {onMount} from "svelte";

    export let url = "";

  onMount(() => {
    const params = new URLSearchParams(window.location.search);
    selectedCategory.set(params.get('category') || '');
    searchQuery.set(params.get('search') || '');
    sortOption.set(params.get('sort') || 'default');
  });
</script>

<style>

</style>

<Router {url}>
    <Header />

    <main>
        <Route path="/" component={ProductList} />
    </main>
</Router>
