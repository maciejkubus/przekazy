<script lang="ts">
	import { onMount } from "svelte";
	import Item from "./Item.svelte";

    export let orders: number[] = []
    let items = [
        { nominal: 200, quantity: 0 },
        { nominal: 100, quantity: 0 },
        { nominal: 50, quantity: 0 },
        { nominal: 20, quantity: 0 },
        { nominal: 10, quantity: 0 },
        { nominal: 5, quantity: 0 },
        { nominal: 2, quantity: 0 },
        { nominal: 1, quantity: 0 },
        { nominal: 0.5, quantity: 0 },
        { nominal: 0.2, quantity: 0 },
        { nominal: 0.1, quantity: 0 },
        { nominal: 0.05, quantity: 0 },
        { nominal: 0.02, quantity: 0 },
        { nominal: 0.01, quantity: 0 },
    ]

    function divide(val:number) {
        let sum = val
        items.forEach(item => {
            let quantity = Math.floor(sum/item.nominal)
            sum -= quantity*item.nominal
            item.quantity += quantity
        })
    }

    onMount(() => {
        orders.forEach(divide)
        items = [...items]
    })
</script>

<table class="border-2 border-white">
    {#each items as item}
        <tr>
            <td class="p-1">{item.nominal} zł</td>
            <td class="p-1">{item.quantity}</td>
        </tr>
    {/each}
</table>