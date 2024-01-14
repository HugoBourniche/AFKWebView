
<script>
    // Bind string
    import BindMedia from "./Binding/BindMedia.svelte";
    import BindThis from "./Binding/BindThis.svelte";

    let name = '';

    // Bind Number
    let a = 1;
    let b = 2;

    // Bind CHeckbox
    let yes = false;

    // Bind Radio and multi select and checkbox group
    let scoops = 1;
    let menu = ['Mint choc chip', 'Raspbewy', 'Strawbewy'];
    let flavours = [];

    function join(flavours) {
        if (flavours.length === 1) return flavours[0];
        return `${flavours.slice(0, -1).join(', ')} and ${flavours[flavours.length - 1]}`;
    }

    // Bind Text Area
    let value = 'Oui.';

    // Bind selector
    let questions = [
        { id: 1, text: `Where did you go to school?` },
        { id: 2, text: `What is your mother's name?` },
        { id: 3, text: `What is another personal fact that an attacker could easily find with Google?` }
    ];

    let selected;

    let answer = '';

    function handleSubmit() {
        alert(`answered question ${selected.id} (${selected.text}) with "${answer}"`);
    }

    // Content Editable
    let html = '<p>Me goes <br/></p>';

    // Block Binding
    let todos = [
        { done: false, text: 'finish Svelte tutorial' },
        { done: false, text: 'build an app' },
        { done: false, text: 'world domination' }
    ];

    function add() {
        todos = todos.concat({ done: false, text: '' });
    }

    function clear() {
        todos = todos.filter(t => !t.done);
    }

    $: remaining = todos.filter(t => !t.done).length;

    // Bind Dimension
    let w;
    let h;
    let size = 42;
    let text = 'edit me';

    // Bind Component
    import BindComponent from './Binding/BindComponent.svelte';

    let pin;
    $: view = pin ? pin.replace(/\d(?!$)/g, '•') : 'enter your pin';

    function handleSubmitComp() {
        alert(`submitted ${pin}`);
    }

    // Bind Component Instance
    import BindComponentInstance from "./Binding/BindComponentInstance.svelte";

    let field;

</script>
<div id="bind string">
    <h1>Bind String : </h1>
    <input bind:value={name}>

    {#if name !== ''}
        <h2>Hello {name}!</h2>
    {/if}
</div>
<div id="bind-numbers">
    <h1>Binding number</h1>

    <label>
        <input type=number bind:value={a} min=0 max=10>
        <input type=range bind:value={a} min=0 max=10>
    </label>

    <label>
        <input type=number bind:value={b} min=0 max=10>
        <input type=range bind:value={b} min=0 max=10>
    </label>

    <p>{a} + {b} = {a + b}</p>
</div>
<div id="bind-checkbox">
    <h1>Binding Checkbox</h1>

    <label>
        <input type=checkbox bind:checked={yes}>
        {#if yes}
            Yes! Send me regular email spam
        {:else}
            No send me nothing
        {/if}
    </label>
</div> <!-- Bind Checkboux -->
<div id="bind-radio">
    <h1>Binding Radio</h1>

    <label>
        <input type=radio group={scoops} name="scoops" value={1}>
        One scoop
    </label>

    <label>
        <input type=radio group={scoops} name="scoops" value={2}>
        Two scoops
    </label>

    <label>
        <input type=radio group={scoops} name="scoops" value={3}>
        Three scoops
    </label>

    <h2>Flavours</h2>

    {#each menu as flavour}
        <label>
            <input type=checkbox bind:group={flavours} name="flavours" value="{flavour}">
            {flavour}
        </label>
    {/each}

    {#if flavours.length === 0}
        <p>Please select at least one flavour</p>
    {:else if flavours.length > scoops}
        <p>Can't order more flavours than scoops!</p>
    {:else}
        <p>
            You ordered {scoops} {scoops === 1 ? 'scoop' : 'scoops'}
            of {join(flavours)}
        </p>
    {/if}
</div> <!-- Bind Radios et Checkboux -->
<div id="bind-textarea">
    <h1>Bind TextArea</h1>
    <p>{value}</p>
    <textarea bind:value={value}></textarea>
</div>
<div id="Bind selector">

    <h1>Bind Selector</h1>

    <form on:submit|preventDefault={handleSubmit}>
        <select bind:value={selected} on:change="{() => answer = ''}">
            {#each questions as question}
                <option value={question}>
                    {question.text}
                </option>
            {/each}
        </select>

        <input bind:value={answer}>

        <button disabled={!answer} type=submit>
            Submit
        </button>
    </form>

    <p>selected question {selected ? selected.id : '[waiting...]'}</p>
</div> <!-- Bind Select -->
<div id="multiple-select">

    <h2>Size</h2>

    <label>
        <input type=radio bind:group={scoops} value={1}>
        One scoop
    </label>

    <label>
        <input type=radio bind:group={scoops} value={2}>
        Two scoops
    </label>

    <label>
        <input type=radio bind:group={scoops} value={3}>
        Three scoops
    </label>

    <h2>Flavours</h2>

    <select multiple bind:value={flavours} class="custom-select custom-select-lg mb-3">
        {#each menu as flavour}
            <option value={flavour}>
                {flavour}
            </option>
        {/each}
    </select>

    {#if flavours.length === 0}
        <p>Please select at least one flavour</p>
    {:else if flavours.length > scoops}
        <p>Can't order more flavours than scoops!</p>
    {:else}
        <p>
            You ordered {scoops} {scoops === 1 ? 'scoop' : 'scoops'}
            of {join(flavours)}
        </p>
    {/if}

</div> <!-- Bind Multi Select -->
<div id="contenteditable">
    <div contenteditable="true" bind:innerHTML={html}></div>
    <pre>{html}</pre>
</div>
<div id="block-binding">
    <h1>Bind blocks</h1>

    {#each todos as todo}
        <div class:done={todo.done}>
            <input
                    type=checkbox
                    bind:checked={todo.done}
            >

            <input
                    placeholder="What needs to be done?"
                    bind:value={todo.text}
            >
        </div>
    {/each}

    <p>{remaining} remaining</p>

    <button on:click={add}>
        Add new
    </button>

    <button on:click={clear}>
        Clear completed
    </button>
</div>
<div id="bind-media">
    <BindMedia />
</div>
<div id="bind-dimension">
    <input type=range bind:value={size}>
    <input bind:value={text}>

    <p>size: {w}px x {h}px</p>

    <div bind:clientWidth={w} bind:clientHeight={h}>
        <span style="font-size: {size}px">{text}</span>
    </div>
</div>
<div id="bind-this">
    <h1>Bind this</h1>
    <BindThis/>
</div>
<div id="bind-component">
    <h1>Bind Component</h1>
    <h1 style="color: {pin ? '#333' : '#ccc'}">{view}</h1>

    <BindComponent bind:value={pin} on:submit={handleSubmitComp}/>
</div> <!-- Bind Component -->
<div id="bind-component-instance">
    <h1>Bind Component Instance</h1>
    <BindComponentInstance bind:this={field} />
    <button on:click="{() => field.focus()}">
        Focus field
    </button>
</div>