<script>
    export let link = "#";

    $: display = link != "#";

    function resetLink() {
        link = "#"
    }
</script>

<style>
    a {
        color: white;
    }
</style>

{#if display}
<a on:click={resetLink} download href={link}>Download</a>
{/if}