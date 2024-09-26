
<script>
    import {navigate} from "svelte-routing";
    import CharacterCard from "./CharacterCard.svelte";
    import CustomTabs from "../CustomTabs.svelte";
    import CharacterStats from "./CharacterStats.svelte";

    export let name;

    const backArrow = '<';
    const tabs = ['Stats', 'Friendship'];
    let selectedTab = tabs[0];

    function back() {
        navigate('/');
    }

    function updateView(event) {
        data = getData(event.detail.charName);
    }

    async function getData(name) {
        console.log("Get Data of : " + name);
        name = name.replace(' & ', ' and ');
        const res = await fetch(process.env.BACK_URL + 'character?name=' + name);
        const text = await res.text();
        if (res.ok) {
            console.log(JSON.parse(text));
            return JSON.parse(text);
        } else {
            throw new Error(text);
        }
    }

    let data = getData(name);

</script>

<main>
    <div>
        <h1> <span class="back" on:click={back}>{backArrow} </span> {name}</h1>

        <!-- replace this element -->
        {#await data}
            <p>...waiting</p>
        {:then character}
            <div class="details">
                <div class="details header">
                    <img class="icon heroe {character.type.toLowerCase()} {character.classe.toLowerCase()}" src="/resources/img/heroes/{character.name}.png" alt="{character.name}">
                    <div class="name">
                        <div>{character.name}</div>
                        <div>{character.fullName}</div>
                    </div>
                </div>
                <div class="details characteristic">
                    <img class="icon" src="/resources/img/icons/{character.faction}.png" alt="{character.faction}">
                    <div class="name">{character.faction}</div>
                </div>
                <div class="details characteristic">
                    <img class="icon" src="/resources/img/icons/{character.type}.png" alt="{character.type}">
                    <div class="name">{character.type}</div>
                </div>
                <div class="details characteristic">
                    <img class="icon" src="/resources/img/icons/{character.classe}.png" alt="{character.classe}">
                    <div class="name">{character.classe}</div>
                </div>
                <div class="details characteristic">
                    <img class="icon" src="/resources/img/icons/{character.role}.png" alt="{character.role}">
                    <div class="name">{character.role}</div>
                </div>
                <div class="details characteristic">
                    <img class="icon" src="/resources/img/icons/{character.rank}.png" alt="{character.rank}">
                    <div class="name">Rank</div>
                </div>
            </div>
            <CustomTabs tabs="{tabs}"  bind:selectedTab="{ selectedTab }"/>

            {#if selectedTab === tabs[0] }
                <CharacterStats characterStats="{character.characterStats}"/>
            {/if}
            {#if selectedTab === tabs[1] }
                <div class="lists">
                    {#each character.relationship as relations}
                        {#if character[relations[0]].length > 0}
                            <div class="list-char {relations[0]}">
                                <h2>{relations[1]}</h2>
                                <div class="cards">
                                    {#each character[relations[0]] as friend}
                                        <CharacterCard character="{friend}" on:update={updateView}/>
                                    {/each}
                                </div>
                            </div>
                        {/if}
                    {/each}
                </div>
            {/if}
        {:catch error}
            <p style="color: red">{error.message}</p>
        {/await}
    </div>
</main>

<style>

    h1 {
        color: #613a05;
        transition: color 300ms;
    }

    .back {
        position: absolute;
        cursor: pointer;
        transform: translateX(-50px);
        -webkit-transition: 300ms ease-in-out;
    }

    .back:hover {
        color: #462902;
        -webkit-transform: translateX(-60px);
    }

    .details {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        padding: 10px;
    }

    .header {
        text-align: left;
    }

    .name {
        padding: 15px;
        font-size: 20px;
    }

    .icon {
        border-radius: 50%;
        width: 100px;
        height: 100px;
    }

    .characteristic img {
        width: 75px;
        height: 75px;
    }

    .cards {
        display: flex;
        flex-wrap: wrap;
    }

    .lists {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-evenly;
        padding: 12px;
    }

    .list-char {
        border: solid 2px;
        border-radius: 24px;
    }

    .friends {
        background-color: #caffb4;
        border-color: #327a1d;
    }

    .friends h2 {
        color: #327a1d;
    }

    .bullies {
        background-color: #e6b4ff;
        border-color: #741d7a;
    }

    .bullies h2 {
        color: #741d7a;
    }

    .enemies {
        background-color: #ffb4b4;
        border-color: #7a1d1d;
    }

    .enemies h2 {
        color: #7a1d1d;
    }
</style>
