<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    export let data;

    // Filtres:
    let select = {
        factions: [],
        types: [],
        classes: [],
        roles: [],
        ranks: []
    }

    const selectKeys = [];
    for (let selectKey in select) {
        selectKeys.push(selectKey);
    }
    cocher();

    function selectOneItem(selectKey, itemId) {
        if (select[selectKey].length === 1 && select[selectKey][0] === itemId) {
            select[selectKey] = data[selectKey]
        } else {
            select[selectKey] = [itemId]
        }
    }

    function decocher() {
        for (let selectKey in select) {
            select[selectKey] = [];
        }
    }

    function cocher() {
        for (let selectKey in select) {
            const elements = data.activeFilter[selectKey]
            select[selectKey] = (elements.length > 0 ? elements : data[selectKey]);
        }
    }

    function filter() {
        console.log(select);
        dispatch('filter', {filters: select});
    }

</script>

<div>
    <div class="container">
        {#each selectKeys as key}
            <div class="list {key}">
                {#each data[key] as element}
                    <label class="image-checkbox" title="{element}">
                        <img class="icon {select[key].includes(element) ? '' : 'disabled'}" src="/resources/img/icons/{element}.png"
                             alt="{element}" on:dblclick={selectOneItem(key, element)}/>
                        <input id="{element}-check" class="hide" bind:group={select[key]} type="checkbox" value="{element}"/>
                    </label>
                {/each}
            </div>
        {/each}
    </div>
    <input class="btn btn-secondary" on:click={cocher} type="button" value="Tout cocher"/>
    <input class="btn btn-secondary" on:click={decocher} type="button" value="Tout décocher"/>
    <input class="btn btn-primary" on:click={filter} type="submit" value="Filtrer"/>

</div>

<style>
    .container {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        padding: 10px;
    }

    .list {
        display: flex;
        flex-wrap: wrap;
        padding: 5px;
        margin: 3px;
        border: #000000 solid 3px;
        border-radius: 12px;
    }

    /*Filter Icon*/
    .factions {
        border-color: #029f9a;
        background-color: #b5f4ff;
    }
    .types {
        border-color: #129f02;
        background-color: #b5ffc1;
    }
    .classes {
        border-color: #12029f;
        background-color: #b7b5ff;
    }
    .roles {
        border-color: #9f0202;
        background-color: #ffb5b5;
    }
    .ranks {
        border-color: #95029f;
        background-color: #edb5ff;
    }
    .ranks img {
        border-radius: 50%;
    }

    /*Filter Icon*/
    .image-checkbox {
        margin: 4px;
    }
    img {
        width: 45px;
        cursor: pointer;
    }

    .disabled {
        -webkit-filter: grayscale(100%);
    }

    .hide {
        display:none;
    }
</style>