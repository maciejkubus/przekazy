<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let id = 0;
	const dispatch = createEventDispatcher();
	export let value: number | null = null;
	export let index: number | null = null;

	function change(e: KeyboardEvent) {
		if (!value) return;

		value = parseFloat(value.toFixed(2));

		dispatch('change', {
			id,
			value
		});
	}

	function isEnter(e: KeyboardEvent) {
		if (e.key == 'Enter' || e.code == 'Enter') {
			dispatch('new');
		}
	}

	function remove() {
		dispatch('remove', id);
	}
</script>

<div class="p-4 w-full border-b-2 border-white border-dashed flex gap-2 items-center">
	<h3 class="h3 text-4xl font-bold">
		<slot></slot>
	</h3>
	<input
		type="number"
		class="w-full bg-transparent outline-0 !ring-0 shadow-none border-0 text-2xl p-0"
		placeholder="0"
		tabindex={index}
		id={'#' + id}
		on:keyup={change}
		on:keydown={isEnter}
		bind:value
		min="0"
	/>
	<div class="text-2xl">zł</div>
	<button
		class="pl-4 text-error-700 hover:text-error-500 font-bold text-2xl"
		on:click={remove}
		tabindex="-1"
	>
		❌
	</button>
</div>
