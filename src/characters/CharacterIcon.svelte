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


</script>


<img class="icon heroe {character.type.toLowerCase()} {character.classe.toLowerCase()}" src="/resources/img/heroes/{character.name}.png" alt="{character.name}" on:click={route}>

<style>

    a {
        text-decoration: none;
        text-decoration: initial;
    }

    text {
        color: black;
    }

    img {
        border-radius: 50%;
        border: #00000000 solid 4px;
    }

    .heroe {
        width: 100px;
        margin: 12px;
        cursor: pointer;
        -webkit-transition: 100ms ease-in-out;
    }

    .heroe:hover {
        -webkit-transform: scale(1.10);
        box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12);
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