<script>

    import TeamDisplay from "../teams/TeamDisplay.svelte";

    export let teamWinner;
    export let teamLoser;
</script>

<div class="container">

    <div class="winning">
        <TeamDisplay characterList="{teamWinner.characterResponses}" />
    </div>
    <div>VS</div>
    <div class="losing">
        <TeamDisplay characterList="{teamLoser.characterResponses}" />
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