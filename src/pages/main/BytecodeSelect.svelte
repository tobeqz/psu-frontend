<script lang="ts">
    export let selected = "Default";

    const options = [
        "Default",
        "Chinese",
        "Arabic",
        "Korean",
        "Emoji",
        "Emoji 2",
        "Greek",
        "Symbols 1",
        "Symbols 2",
        "Symbols 3"
    ]
</script>

<style>
    select {
        padding: 7px;
        border: solid 2px #d1d1d1;
        color: #d1d1d1;
        border-radius: 4px;
        background-color: rgba(0, 0, 0, 0);
        outline: none;
    }

    select::-ms-expand {
        display: none;
    }

    option {
        color: black;
        background-color: rgba(0,0,0,0);
    }

    div {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        width: 250px;
    }
</style>

<div>
    <p>Bytecode</p>
    <select bind:value={selected}>
        {#each options as option_name}
            <option value={option_name}>{option_name}</option>
        {/each}
    </select>
</div>