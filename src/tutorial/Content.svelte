<script>
    export let name = 'None';
    let count = 0;
    let numbers = [];
    $: doubled = count *2;
    $: {
        console.log('Counted: ' + count);
        if (count > 10) {
            alert('Double: ' + doubled);
        }
    }

    function incrementCount() {
        count++;
        if (!numbers.includes(count)) {
            numbers = [...numbers, count];
        }
    }
    $: sum = numbers.reduce((t, n) => t + n, 0);
</script>


<h1>Hello {name}!</h1>
<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
<div>
    <button on:click={incrementCount}>
        {count} nb click{count > 1 ? 's' : ''}
    </button>
    <p>{numbers.join(' + ')} = {sum}</p>
</div>
