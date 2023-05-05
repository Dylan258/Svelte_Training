<script>
    import { createEventDispatcher } from "svelte";
    import TodoCard from "./todoCard.svelte";
    import NewTodoCard from "./newTodoCard.svelte"
    export let todos = [];
    
    const dispatch = createEventDispatcher();

    const handleNewTodo = () => {
        console.log('datalist.svelte');
        dispatch('refresh');
    }
    
</script>

<div class="grid gap-4 grid-cols-4 justify-center">
    {#each todos as todo}
        <TodoCard {todo} />
    {/each}
    <NewTodoCard on:addNewTodo={handleNewTodo}/>
</div>
