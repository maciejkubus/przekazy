<script lang="ts">
	export const prerender = true;
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

		setTimeout(() => {
			const elToFocus: HTMLInputElement | null = document.querySelector(
				'input[tabindex="' + (items.length - 1) + '"]'
			);

			if (elToFocus) elToFocus.focus();
		});
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

	function goBack() {
		done = false;
	}
</script>

<div class="w-full h-full mx-auto flex justify-center items-center">
	<div class="w-full">
		{#if !done}
			<h1 class="h1 text-4xl font-bold py-8">Enter orders</h1>
			<div
				class="w-full flex flex-col justify-center items-center border-t-2 border-white border-dashed"
			>
				{#each items as item, index}
					<Item
						id={item.id}
						value={item.value}
						on:change={change}
						on:remove={remove}
						on:new={add}
						{index}
					>
						#{index + 1}
					</Item>
				{/each}
			</div>
			<div class="pt-8 flex">
				<button
					class="p-4 w-full text-center bg-primary-500 hover:bg-primary-400 text-xl font-bold"
					on:click={add}
				>
					Add
				</button>
				<button
					class="p-4 w-full text-center bg-secondary-500 hover:bg-secondary-400 text-xl font-bold"
					on:click={submit}
				>
					Calculate
				</button>
			</div>
		{:else}
			<button
				class="text-1xl mt-8 mb-12 rounded-lg bg-surface-500 flex justify-center items-center gap-4 py-2 px-4 hover:bg-surface-400"
				on:click={goBack}
			>
				<span class="text-3xl">&#10554;</span>
				<span>Back</span>
			</button>
			<h1 class="h1 text-4xl pb-8 font-bold">Summary</h1>
			<Summary orders={items.map((i) => parseFloat(i.value ? i.value : 0))}></Summary>
		{/if}
	</div>
</div>
