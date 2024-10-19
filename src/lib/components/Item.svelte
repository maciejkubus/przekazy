<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let id = 0;
	const dispatch = createEventDispatcher();
	export let value: number | null = null;

	function change() {
		dispatch('change', {
			id,
			value
		});
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
		id={'#' + id}
		on:keyup={change}
		bind:value
		min="0"
	/>
	<div class="text-2xl">zł</div>
	<button class="pl-4 text-error-700 hover:text-error-500 font-bold text-2xl" on:click={remove}
		>[X]</button
	>
</div>
