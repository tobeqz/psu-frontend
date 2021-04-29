<script lang="ts">
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    function click() {
        dispatch("click");
    }
</script>

<style>
    button {
        width: 250px;
        height: 40px;
        border-radius: 20px;
        border: none;
        background-color: #098352;
        color: white;
        font-weight: bold;
        cursor: pointer;
        transition: transform .2s;
    }

    button:hover {
        transform: scale(1.1, 1.1);
    }
</style>

<button on:click={click}>
    Obfuscate
</button>