<script lang="ts">
	import { onMount } from 'svelte';
	import Item from './Item.svelte';

	export let orders: number[] = [];
	let sum = 0;
	let items = [
		{ nominal: 200, label: '2 zł', quantity: 0 },
		{ nominal: 100, label: '1 zł', quantity: 0 },
		{ nominal: 50, label: '5 zł', quantity: 0 },
		{ nominal: 20, label: '2 zł', quantity: 0 },
		{ nominal: 10, label: '1 zł', quantity: 0 },
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
	{#each items as item}
		<div class="p-4 border-b-2 border-white border-dashed flex items-end">
			<div class="w-full text-right text-2xl">{item.label}</div>
			<div class="px-2 text-lg">x</div>
			<div class="w-full text-2xl">{item.quantity}</div>
		</div>
	{/each}
	<div class="text-right py-8 px-4 text-4xl font-bold">
		{sum.toFixed(2)} zł
	</div>
</div>
