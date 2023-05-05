<script>
    import Datalist from "$src/base_components/data-series/data-lists/datalist.svelte";
    import { onMount } from "svelte";

    const getTodos = async () => {
        return (await fetch('http://localhost:3000/todos')).json()
    }
    
    const handleRefresh = async () => {
        console.log('todos.svelte');
        await getTodos();
    }
</script>

<main class="grid justify-center">
    {#await getTodos()}
        <button class="btn loading">loading</button>
    {:then todos}
        <Datalist {todos} on:refresh{handleRefresh}/>
    {/await}
</main>
