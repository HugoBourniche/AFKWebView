
<script>

    import TeamDisplay from "./TeamDisplay.svelte";
    export let teams;
    export let empty;
</script>


{#if teams.length > 0}
    <div class="container">
        <h2>{teams.length} Teams</h2>
        {#each teams as team}
            <TeamDisplay characterList="{team.characterResponses}"/>
        {/each}
    </div>
{:else}
    <div>{empty}</div>
{/if}

<style>

</style>