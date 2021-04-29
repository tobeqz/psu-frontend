<script lang="ts">
    import {fade} from "svelte/transition";
    export let name: string;
    export let value = false;

    function toggle() {
        value = !value
    }

    $: clickedClass = value ? "toggled_on" : ""
</script>

<style>
    .container {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center; 
        width: 250px;
        cursor: pointer;
    }

    .toggle_checkbox {
        border: solid 2px #d1d1d1;
        border-radius: 4px;
        width: 20px;
        height: 20px;
        transition: .2s;
    }

    .toggled_on {
        background-color: #0a9b61;
    }
</style>

<div class="container" on:click={toggle}>
    <p>{name}</p>
    <div transition:fade class="toggle_checkbox {clickedClass}">

    </div>
</div>