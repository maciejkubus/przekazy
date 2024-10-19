<script lang='ts'>
	import { createEventDispatcher } from "svelte";

    export let defaultValue = 0;
    export let id = 0;
    const dispatch = createEventDispatcher()
    let value = defaultValue;

    function change() {
        dispatch("change", {
            id, 
            value
        })
    }
</script>

<div class="p-4 w-full border-b-2 border-black">
    <input type="number" class="w-full text-center text-black" on:keyup={change} bind:value={value}>
</div>