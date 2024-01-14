<script>

    import CharacterCard from "../characters/CharacterCard.svelte";
    import CustomTabs from "../CustomTabs.svelte";
    import TeamFightTab from "./TeamFightTab.svelte";
    import TeamsDisplayTab from "./TeamsDisplayTab.svelte";

    const tabs = ['Overview', 'Teams', 'Combats Gagnés', 'Combats Perdus'];
    let selectedTab = tabs[0];

	async function getTeam() {
        const res = await fetch('http://localhost:8080/current-team');
        const text = await res.text();
        if (res.ok) {
            console.log(JSON.parse(text));
            return JSON.parse(text);
        } else {
            throw new Error(text);
        }
    }

    function updateData() {
        team = getTeam();
    }

    let team = getTeam();
</script>


<main>
	<h1>Ma Team</h1>

	<!-- replace this element -->
    {#await team}
        <p>...waiting</p>
    {:then teamBlob}
        <div class="container">
            {#each teamBlob.characters as character}
                <CharacterCard character="{character}" on:teamUpdate={updateData}/>
            {/each}
            {#if teamBlob.characters.length < 5}
            <a href="/">
	            <div class="card brown">
				    <div class="card-body">
				        <h5 class="text card-title">+</h5>
				        <h6 class="text card-subtitle">Ajouter un personnage à l'équipe</h6>
				    </div>
				</div>
			</a>
            {/if}
        </div>
        {#if (teamBlob.characters.length > 0)}
            <CustomTabs tabs="{ tabs }" bind:selectedTab="{ selectedTab }" />
            {#if selectedTab === tabs[0]}
                <div>
                    Équipes: {teamBlob.teams.length}
                </div>
                <div>
                    Combats gagnés: {teamBlob.winning.length}
                </div>
                <div>
                    Combats perdus: {teamBlob.lost.length}
                </div>
                <div>
                    Win rate: {  Math.round( ( teamBlob.winning.length / (teamBlob.lost.length + teamBlob.winning.length) ) * 100 ) } %
                </div>
            {/if}
            {#if selectedTab === tabs[1]}
                <TeamsDisplayTab teams="{teamBlob.teams}" empty="Il n'existe aucune donnée concernant l'équipe que vous avez composé"/>
            {/if}
            {#if selectedTab === tabs[2]}
                <TeamFightTab title="Combats Gagnés" fightsArray="{teamBlob.winning}" emptyMessage="Cette équipe n'a gagné aucun combat"/>
            {/if}
            {#if selectedTab === tabs[3]}
                <TeamFightTab title="Combats Perdus" fightsArray="{teamBlob.lost}" emptyMessage="Cette équipe n'a perdu aucun combat"/>
            {/if}
        {/if}
    {:catch error}
        <p style="color: red">{error.message}</p>
    {/await}
</main>


<style>
	
	/*Pasted from home*/
	h1 {
        color: #613a05;
        padding: 12px;
    }

	.container {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        margin-top: 12px;
	}

	/* Pasted from character card */
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
        border: 1px solid;
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

    .brown {
        color: #7e4c09;
        border-color: #7e4c09;
    }
</style>