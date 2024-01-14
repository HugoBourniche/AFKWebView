<script>
    export let tabs;
    export let selectedTab;


    const widthProportion = 100 / tabs.length + '%';

    function tabClick(tabName) {
        selectedTab = tabName;
    }
</script>



<div class="container">
    {#each tabs as tabName}
        <h4 class="tab-item { (selectedTab === tabName ? 'selected' : '') }" style="width: {widthProportion}" on:click={tabClick(tabName)}>{tabName}</h4>
    {/each}
</div>


<style>

    .container {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        margin-top: 12px;
        margin-bottom: 12px;
    }

    .tab-item {
        /*width: 25%;*/
        margin: auto;
        padding: 12px;
        -webkit-transition: 100ms ease-in-out;
        background-color: #00000000;
        color: #613a05;
        cursor: pointer;
        border-top: 1px solid #6c6c6c;
        border-bottom: 1px solid #6c6c6c;
    }

    .tab-item:hover {
        color: white;
        background-color: rgba(97, 58, 5, 0.66);
    }

    .tab-item {

    }

    .selected {
        color: white;
        background-color: rgba(97, 58, 5, 0.66);
        cursor: auto;
    }
</style>