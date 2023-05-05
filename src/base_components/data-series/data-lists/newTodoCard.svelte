<script>
    import { createEventDispatcher } from 'svelte';
    import { fade } from 'svelte/transition';
    let title;
    let description;
    const dispatch = createEventDispatcher();

    const saveNewTodo = async () => {
        const todo = {
            title: title,
            description: description,
            completed: false,
        };
        const result = await fetch(
            'http://localhost:3000/todos', {
                method: "POST",
                headers: {
                    Accept: "application.json",
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(todo)
            }
        );
        if (result.ok) {
            dispatch('addNewTodo');
        }
    };


</script>

<div transition:fade class="card w-96 bg-primary text-primary-content">
    <div class="card-body">
        <input bind:value={title} class="card-title bg-transparent" type="text" placeholder="Title"/>
        <textarea bind:value={description} class="bg-transparent" rows="10" id="newCardDescription" placeholder="Description"/>
        <div class="card-actions justify-end">
            <button type="button" class="btn" on:click={saveNewTodo}>Save</button>
        </div>
    </div>
</div>

<style>
    input:focus, textarea:focus {
        outline: none;
    }
</style>
