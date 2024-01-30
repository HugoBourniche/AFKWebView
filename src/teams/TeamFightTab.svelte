
<script>

    import FightDisplay from "../fights/FightDisplay.svelte";

    export let title;
    export let fightsArray;
    export let emptyMessage;

    function computeFights() {
        console.log("Compute fight");
    }
</script>


<div>
    {#if fightsArray.length > 0}
        <hr>
        <div class="container">
            <h2>{fightsArray.length} {title}</h2>
            {#each fightsArray as fight}
                <FightDisplay fight="{fight}"/>
                <hr>
            {/each}
        </div>
    {:else}
        <div>{emptyMessage}</div>
        <button on:click={computeFights}>Calculer un résultat</button>
    {/if}
</div>

<style>

</style>