<script lang="ts">
	let toDoList: todos[] = [];

	interface todos {
		content: string;
		editing: boolean;
		checked: boolean;
	}

	let newTodo = '';

	function addToDo() {
		if (newTodo !== '') {
			toDoList = [...toDoList, { content: newTodo, editing: false, checked: false }];
			newTodo = '';
		}
	}

	function deleteToDo(i: number) {
		toDoList.splice(i, 1);
		toDoList = toDoList;
	}
</script>

<div class="container mx-auto p-8 space-y-8">
	<h1 class="h1">To Do List</h1>
	<input class="input w-4/12" type="text" placeholder="new todo here" bind:value={newTodo} />
	<button class="btn variant-filled-primary" on:click={addToDo}>Add</button>
	<hr />
	{#each toDoList as toDo, i}
		<div>
			{#if toDo.editing}
				<input class="input w-4/12" type="text" bind:value={toDo.content} />
			{:else}
				<input type="checkbox" class="checkbox" bind:checked={toDo.checked} />
				<span class="text-lg px-4">{toDo.content}</span>
			{/if}

			{#if toDo.editing}
				<button class="btn variant-filled-secondary" on:click={() => (toDo.editing = false)}
					>save</button
				>
			{:else}
				<button class="btn variant-filled-secondary" on:click={() => (toDo.editing = true)}
					>edit</button
				>
			{/if}

			<button class="btn variant-filled-secondary" on:click={() => deleteToDo(i)}>delete</button>
		</div>
	{/each}
</div>
