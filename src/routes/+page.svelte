<script lang="ts">
	import Item from '$lib/components/Item.svelte';
	import Summary from '$lib/components/Summary.svelte';
	let items: any[] = [];
	let money = 0;
	let done = false;

	function add() {
		items = [
			...items,
			{
				id: Date.now(),
				value: null
			}
		];
	}

	function sum() {
		money = 0;
		items.forEach((item) => (money += item.value ? item.value : 0));
	}

	function change(event: any) {
		const item = items.find((i) => i.id == event.detail.id);
		item.value = event.detail.value;
		sum();
	}

	function remove(event: any) {
		items = [...items.filter((i) => i.id != event.detail)];
	}

	function submit() {
		done = true;
	}
</script>

<div class="w-full h-full mx-auto flex justify-center items-center">
	<div class="w-full">
		<h1 class="h1 text-4xl py-8">Przekazy</h1>
		{#if !done}
			<div
				class="w-full flex flex-col justify-center items-center border-t-2 border-white border-dashed"
			>
				{#each items as item, index}
					<Item id={item.id} value={item.value} on:change={change} on:remove={remove}>
						#{index + 1}
					</Item>
				{/each}
			</div>
			<div class="pt-8 flex">
				<button
					class="p-4 w-full text-center bg-primary-500 hover:bg-primary-400 text-xl font-bold"
					on:click={add}
				>
					Dodaj
				</button>
				<button
					class="p-4 w-full text-center bg-secondary-500 hover:bg-secondary-400 text-xl font-bold"
					on:click={submit}
				>
					Oblicz
				</button>
			</div>
		{:else}
			<Summary orders={items.map((i) => parseFloat(i.value ? i.value : 0))}></Summary>
		{/if}
	</div>
</div>
