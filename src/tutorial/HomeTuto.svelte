<script>
    import Content from './Content.svelte';
    import Character from './CharacterTuto.svelte';
    import Async from "./Async.svelte";
    import Events from "./Events.svelte";
    import Binding from "./Binding.svelte";
    import Saber from "../saber/Saber.svelte";

    export let name;

    let img = 'resources/img/madara.gif'
    let isDeleted = false;
    const char = {
        name: 'Rowan',
        classe: 'Intelligence',
        faction: 'Porteur de Lumière'
    }
    const char2 = {
        name: 'Talene',
        classe: 'Rodeur',
        faction: 'Celestial'
    }
    const char3 = {
        name: 'Ezio',
        classe: 'Rodeur',
        faction: 'Dimensionnal'
    }
    const char4 = {
        name: 'Grezhul',
        classe: 'Tank',
        faction: 'Graveborn'
    }
    let characters = [char, char2, char3, char4];

    function remove() {
        characters = characters.slice(1, characters.length);
        isDeleted = true;
    }

    let isLogin = true;
    function logged(event) {
        console.log(event);
        isLogin = event.detail['isLogin'];
    }
</script>

<main>
    <Saber/>
    <Content name="{name}" />
    <Binding />

    <br/>
    <button on:click|once={remove} disabled="{isDeleted}">Delete Char</button>
    {#each characters as character (character.name)}
        <div style="padding: 10px">
            <Character character="{character}"/>
        </div>
    {/each}
    <Async/>
    <Events/>

    <br/>
    <br/>
    <br/>
    <img src="{img}" alt="gif :)">
</main>