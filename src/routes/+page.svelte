<script lang="ts">
	import Item from "$lib/components/Item.svelte";
	import Summary from "$lib/components/Summary.svelte";
	let items: any[] = [];
	let money = 0
	let done = false

	function add() {
		items = [...items, {
			id: Date.now(),
			value: 0
		}]
	}

	function sum() {
		money = 0
		items.forEach(item => money+=item.value)
	}

	function change(event: any) {
		const item = items.find(i => i.id == event.detail.id)
		item.value = event.detail.value
		sum()
	}

	function submit() {
		done = true
	}
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-5 pt-8 w-96">
		<h1 class="h1">Money: {money}</h1>
		{#if !done}
			{#each items as item}
				<Item defaultValue={item.value} id={item.id} on:change={change}></Item>
			{/each}
			<button class="p-4 w-full text-center bg-primary-500 text-xl font-bold" on:click={add}>+</button>
			<button class="p-4 w-full text-center bg-secondary-500 text-xl font-bold" on:click={submit}>=</button>
		{:else}
			<Summary orders={items.map(i => parseFloat(i.value))}></Summary>
		{/if}
	</div>
</div>
