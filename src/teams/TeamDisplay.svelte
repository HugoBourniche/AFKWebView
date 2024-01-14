
<script>
    import CharacterIcon from "../characters/CharacterIcon.svelte";
    export let characterList;
</script>

<div class="container">
    {#each characterList as character, index}
        <CharacterIcon character="{character}"/>
        {#if index === 1}
            <span class="vertical-line"></span>
        {/if}
    {/each}
</div>

<style>

    .container {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        margin-top: 12px;
    }

    .vertical-line {
        margin-right: 25px;
        margin-left: 25px;
    }

</style>