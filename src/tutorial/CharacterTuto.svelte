<script>
    export let character;
    const charImage = `resources/img/heroes/${character?.name}.png`;
</script>

<div class="container">
    <img src="{charImage}" alt="{character.name} icon">
    <div>Name: {character.name}</div>
    <div>Classe: {character.classe}</div>
    <div>Faction: {character.faction}</div>
</div>
