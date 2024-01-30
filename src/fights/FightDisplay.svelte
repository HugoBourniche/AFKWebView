<script>

    import TeamDisplay from "../teams/TeamDisplay.svelte";

    export let fight;

</script>

<div class="container">
    <div>{fight.type}</div>
    <div class="winning">
        <TeamDisplay characterList="{fight.winner.characterResponses}" />
    </div>
    <div>VS</div>
    <div class="losing">
        <TeamDisplay characterList="{fight.loser.characterResponses}" />
    </div>
</div>

<style>

    .container {
        margin-top: 12px;
        background: linear-gradient(#00000000, #f9ddbc 20%, #00000000, #97D7EB 80%, #00000000);
    }

    .winning {
        /*background: linear-gradient(#00000000, #f9ddbc, #00000000);*/
    }

    .losing {
        /*background: linear-gradient(#00000000, #97D7EB, #00000000);*/
    }

</style>