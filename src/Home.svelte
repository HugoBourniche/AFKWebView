<script>

    import Filtres from "./filter/Filters.svelte";
    import CharacterCard from "./characters/CharacterCard.svelte";

    async function getData() {
        const res = await fetch('http://localhost:8080/characters');
        const text = await res.text();
        if (res.ok) {
            console.log(JSON.parse(text));
            return JSON.parse(text);
        } else {
            throw new Error(text);
        }
    }

    async function filterData(event) {
        // request options
        const options = {
            method: 'POST',
            body: JSON.stringify(event.detail.filters),
            headers: {
                'Content-Type': 'application/json'
            }
        }

        const res = await fetch('http://localhost:8080/filterCharacters', options);
        const text = await res.text();
        if (res.ok) {
            console.log(JSON.parse(text));
            data = JSON.parse(text);
        } else {
            throw new Error(text);
        }
    }

    let data = getData();


</script>


<main>
    <h1>Les Personnages</h1>

    <!-- replace this element -->
    {#await data}
        <p>...waiting</p>
    {:then dataBlob}
        <Filtres on:filter={filterData} data="{dataBlob}"/>
        <div class="container">
            {#each dataBlob.characters as character}
                <CharacterCard character="{character}"/>
            {/each}
        </div>
    {:catch error}
        <p style="color: red">{error.message}</p>
    {/await}


</main>

<style>

    h1 {
        color: #613a05;
        padding: 12px;
    }

    .container {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        margin-top: 12px;
    }


</style>