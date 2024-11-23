<script lang="ts">
	import { onMount } from 'svelte';
	import Item from './Item.svelte';

	export let orders: number[] = [];
	let sum = 0;
	let items = [
		{ nominal: 200, label: '200 zł', quantity: 0 },
		{ nominal: 100, label: '100 zł', quantity: 0 },
		{ nominal: 50, label: '50 zł', quantity: 0 },
		{ nominal: 20, label: '20 zł', quantity: 0 },
		{ nominal: 10, label: '10 zł', quantity: 0 },
		{ nominal: 5, label: '5 zł', quantity: 0 },
		{ nominal: 2, label: '2 zł', quantity: 0 },
		{ nominal: 1, label: '1 zł', quantity: 0 },
		{ nominal: 0.5, label: '50 gr', quantity: 0 },
		{ nominal: 0.2, label: '20 gr', quantity: 0 },
		{ nominal: 0.1, label: '10 gr', quantity: 0 },
		{ nominal: 0.05, label: '5 gr', quantity: 0 },
		{ nominal: 0.02, label: '2 gr', quantity: 0 },
		{ nominal: 0.01, label: '1 gr', quantity: 0 }
	];

	function divide(val: number) {
		let sum = val;
		items.forEach((item) => {
			let quantity = Math.floor(sum / item.nominal);
			sum -= quantity * item.nominal;
			item.quantity += quantity;
		});
	}

	onMount(() => {
		orders.forEach(divide);
		items = [...items];

		items.forEach((item) => {
			sum += item.nominal * item.quantity;
		});
	});
</script>

<div>
	<div
		class="flex flex-col justify-center items-center text-2xl w-full border-t-2 border-white border-dashed"
	>
		{#each items as item, index}
			{#if item.quantity > 0}
				<div class="py-2 border-b-2 border-white border-dashed w-full text-center">
					{item.quantity} &times; {item.label} &equals; {(item.quantity * item.nominal).toFixed(2)} zł
				</div>
			{/if}
		{/each}
	</div>
	<div class="text-right py-8 text-4xl font-bold px-8">
		{sum.toFixed(2)} zł
	</div>
</div>
