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
			//this is to avoid 0.1 + 0.2 =  0.30000000000000004 error
			let nominal = item.nominal * 100;

			let quantity = Math.floor(sum / nominal);
			sum -= quantity * nominal;
			item.quantity += quantity / 100;
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

<div class="px-16">
	<table class="mx-auto table table-fixed rounded-none shadow-lg">
		<thead>
			<tr>
				<th class="!text-2xl border-2 border-white px-4 py-2">Quantity</th>
				<th class="!text-2xl border-2 border-white px-4 py-2">Denomination</th>
				<th class="!text-2xl border-2 border-white px-4 py-2">Sum</th>
			</tr>
		</thead>
		<tbody>
			{#each items as item}
				<tr class="table-row">
					<td class="w-20 !text-2xl border-2 border-white px-4 py-2">{item.quantity}</td>
					<td class="w-12 !text-2xl border-2 border-white px-4 py-2">{item.label}</td>
					<td class="w-32 !text-2xl border-2 border-white px-4 py-2">
						{item.quantity * item.nominal} zł
					</td>
				</tr>
			{/each}
		</tbody>
	</table>
	<div class="text-right py-8 px-4 text-4xl font-bold">
		Total: {sum.toFixed(2)} zł
	</div>
</div>
