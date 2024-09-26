<script>
    import {navigate} from "svelte-routing";
    import {createEventDispatcher} from "svelte";

    export let character;

    const dispatch = createEventDispatcher();

    function route() {
        navigate("/character/" + character.name);
        dispatch('update', {
            charName: character.name
        });
    }

    async function addToTeam(event) {
        event.stopPropagation()
        const res = await fetch(process.env.BACK_URL + 'add-character?name=' + character.name.replace("&", "and"))
        const characterPosition = await res.text();
        character.position = parseInt(characterPosition)
        teamUpdate();
    }

    async function removeFromTeam(event) {
        event.stopPropagation()
        const options = {
            method: 'POST',
            body: character.name
        }
        await fetch(process.env.BACK_URL + 'remove-character', options).then(() => {
            character.position = 0
            teamUpdate();
        });
    }

    // TODO envoyer un evenement après suppression d'un personnage de l'équipe selectionnée
    function teamUpdate() {
        dispatch('teamUpdate');
    }

</script>
<div class="card {character.faction.toLowerCase()}" on:click={route}>
    {#if character.position === 0}
        <div class="icon-button add" on:click={addToTeam}>+</div>
    {:else}
        <div class="icon-button remove" on:click={removeFromTeam}>{character.position}</div>
    {/if}
    <img class="rank {character.faction.toLowerCase()}" src="/resources/img/icons/{character.rank}.png" alt="{character.rank}">
    <img class="icon heroe {character.type.toLowerCase()} {character.classe.toLowerCase()}" src="/resources/img/heroes/{character.name}.png" alt="{character.name}">
    <div class="card-body">
        <h5 class="text card-title">{character.name}</h5>
        <h6 class="text card-subtitle mb-2 text-muted">{character.fullName}</h6>
    </div>
    <ul class="list-group list-group-flush">
        <li class="list-group-item background-invisible">
            <img class="icon caracteristics" src="/resources/img/icons/{character.faction}.png" alt="{character.faction}">
            <img class="icon caracteristics" src="/resources/img/icons/{character.type}.png" alt="{character.type}">
            <img class="icon caracteristics" src="/resources/img/icons/{character.classe}.png" alt="{character.classe}">
            <img class="icon caracteristics" src="/resources/img/icons/{character.role}.png" alt="{character.role}">
        </li>
    </ul>
</div>

<style>

    a {
        text-decoration: none;
        text-decoration: initial;

    }

    text {
        color: black;
    }

    .card {
        display: flex;
        position: relative;
        align-items: center;
        justify-content: center;
        border: 0 none;
        margin: 20px 10px 20px 10px;
        padding: 12px;
        width: 12rem;
        -webkit-transition: 100ms ease-in-out;
        cursor: pointer;
    }

    .card:hover {
        -webkit-transform: scale(1.10);
        box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12);
    }

    .card-body {
        height: 90px;
    }

    .card-subtitle {
        color: #aaaaaa;
        font-weight: lighter;
    }

    img {
        border-radius: 8px;
        border: #00000000 solid 4px;
    }

    .heroe {
        width: 100px;
    }

    .card-title {
        -webkit-text-size-adjust: auto;
    }
    .caracteristics {
        width: 45%;
    }

    .background-invisible {
        background-color: #00000000;
    }

    .rank {
        position: absolute;
        bottom: -5%;
        width: 25%;
        border: 2px solid #6c6c6c;
        border-radius: 50%;
    }

    .icon-button {
        position: absolute;
        right: 0;
        font-weight: bold;
        color: #00000055;
        -webkit-transition: 100ms ease-in-out;
    }

    .add {
        top: -15px;
        font-size: 30px;
    }
    .remove {
        top: -4px;
        font-size: 20px;
    }
    .add:hover {
        color: #51ff2355;
    }

    .remove:hover {
        color: #FF233555;
    }

    /* Custom Colors */

    .dimensional {
        background: rgb(255,255,255);
        background: linear-gradient(180deg, rgba(98,101,147,1) 0%, rgba(171,213,202,0.5) 35%, rgba(238,224,165,0.5) 50%, rgba(171,213,202,0.5) 65%, rgba(98,101,147,1) 100%);
        border-color: #626593;
    }

    .celestial {
        background: rgb(255,255,255);
        background: linear-gradient(180deg, rgba(255,255,255,1) 0%, rgba(252,255,186,0.50) 80%, rgba(255,255,255,1) 100%);
        border-color: #FCFFBA;
    }

    .hypogean {
        background: rgb(255,255,255);
        background: linear-gradient(180deg, rgba(0,0,0,0.5) 0%, rgba(52,52,116,0.5) 7%, rgba(159,74,183,0.5) 25%, rgba(242,173,250,0.5) 50%, rgba(159,74,183,0.5) 75%, rgba(52,52,116,0.5) 93%, rgba(0,0,0,0.5) 100%);
        border-color: #3434747F;
    }

    .graveborn {
        background: rgb(255,255,255);
        /*background: linear-gradient(180deg, rgba(0,0,0,0.5) 0%, rgba(26,154,11,0.5) 25%, rgba(189,255,0,1) 50%, rgba(26,154,11,0.5) 78%, rgba(0,0,0,0.5) 100%);    */
        background: radial-gradient(circle, rgba(0,0,0,0.5) 0%, rgba(0,0,0,0.5) 5%, rgba(26,154,11,0.5) 10%, rgba(189,255,0,0.5) 16%, rgba(189,255,0,0.5) 29%, rgba(26,154,11,0.4) 55%, rgba(0,0,0,0.75) 74%, rgba(0,0,0,1) 100%);
        border-color: #000000;

    }

    .mauler {
        background: rgb(255, 255, 255);
        background: radial-gradient(circle, rgba(211,156,64,0.5) 0%, rgba(239,230,186,1) 12%, rgba(224,161,72,0.5) 28%, rgba(246,209,74,1) 39%, rgba(124,79,46,0.5) 100%);
        border-color: #E0A1487F;
    }

    .lightbearer {
        background: rgb(255, 255, 255);
        background: linear-gradient(180deg, rgba(65,102,149,1) 0%, rgba(230,189,116,0.5) 20%, rgba(254,251,186,0.5) 40%, rgba(254,251,186,0.5) 60%, rgba(230,189,116,0.5) 80%, rgba(65,102,149,1) 100%);
        border-color: #416695;
    }

    .wilder {
        background: rgb(255, 255, 255);
        background: radial-gradient(circle, rgba(141,251,157,0.5) 0%, rgba(189,252,223,0.5) 20%, rgba(37,89,68,0.5) 25%, rgba(118,223,147,0.5) 30%, rgba(118,223,147,0.5) 75%, rgba(0,0,0,0.5) 100%);
        border-color: #76DF937F;
    }

    .agility {
        border-bottom-color: #BDDC64;
        border-right-color: #F1F9BC;
    }

    .intelligence {
        border-bottom-color: #97D7EB;
        border-right-color: #CDDEE5;
    }

    .strength {
        border-bottom-color: #E3A4A1;
        border-right-color: #FDF6E6;
    }

    .mage {
        border-top-color: #F1B7EE;
        border-left-color: #BB69C6;
    }

    .ranger {
        border-top-color: #D3E5B6;
        border-left-color: #5EBA3B;
    }

    .support {
        border-top-color: #B7E5F3;
        border-left-color: #7FD1DF;
    }

    .tank {
        border-top-color: #FDFAB4;
        border-left-color: #E9B959;
    }

    .warrior {
        border-top-color: #F9F6AC;
        border-left-color: #ECA069;
    }

</style>