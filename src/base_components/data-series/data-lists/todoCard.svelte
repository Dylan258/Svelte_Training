<script>
    import { scale } from "svelte/transition";
    export let todo = {}

    const toggleCompleted = async () => {
        todo.completed = !todo.completed
        const result = await fetch(
            `http://localhost:3000/todos/${todo.id}`,
            {
                method: 'PUT',
                headers: {
                    Accept: 'application.json',
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(todo)
            }
        )
    }

    const deleteTodo = async () => {
        const result = await fetch(
            `http://localhost:3000/todos/${todo.id}`,
            {
                method: 'DELETE',
                headers: {
                    Accept: 'application.json',
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(todo)
            }
        )
    }
</script>

<div class="card w-96 bg-primary text-primary-content">
    <div class="card-body">
        <h2 class="card-title">{todo.title}</h2>
        <p contenteditable="true">{todo.description}</p>
        <div transition:scale class="card-actions justify-between">
            <button class="btn btn-square btn-delete" on:click={deleteTodo}>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
            </button>
            {#if todo.completed}
            <button type="button" class="btn" on:click={toggleCompleted}>Completed</button>
            {:else}
            <button type="button" class="btn" on:click={toggleCompleted}>Complete</button>
            {/if}
        </div>
    </div>
    <div class="alert alert-success shadow-lg">
        <div>
          <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current flex-shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
          <span>Task completed!</span>
        </div>
    </div>
</div>

<style>
    p:focus, h2:focus {
        outline: none;
    }
    .btn-delete:hover {
        background-color: red;
        border-color: red;
    }
</style>