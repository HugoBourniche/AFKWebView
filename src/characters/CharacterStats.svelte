
<script>

    export let characterStats;

    const winRatePercent = Math.round(characterStats.winRate * 100) + "%";
</script>


<div class="container">
    <div class="child left">
        <h4>Positions</h4>
        {#each Object.keys(characterStats.positionUsage) as key}
            <div class="progress">
                <span>{key}</span>
                <div class="progress-bar bg-success" style="width: {characterStats.positionUsage[key]*100}%" role="progressbar"></div>
            </div>
        {/each}
    </div>
    <div class="child right">
        <div>Appartient à {characterStats.nbTeams} équipes</div>
        <div>Combattu {characterStats.nbFights} fois</div>
        <div>Win rate: {winRatePercent}</div>
    </div>
</div>

<style>

    .container {
        display: flex;
        align-items: center;
        justify-content: space-around;
    }

    .child {
        display: flex;
        flex-direction: column;
        padding: 3px;
    }

    .left {
        justify-content: left;
    }
</style>