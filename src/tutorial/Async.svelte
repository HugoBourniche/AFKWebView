<script>
    async function getRandomNumber() {
        const res = await fetch(process.env.BACK_URL + 'characters');
        const text = await res.text();

        if (res.ok) {
            return text;
        } else {
            throw new Error(text);
        }
    }

    let promise = null;

    function handleClick() {
        promise = getRandomNumber();
    }
</script>

<button on:click={handleClick}>
    generate random number
</button>

<!-- replace this element -->
{#await promise}
    <p>...waiting</p>
{:then number}
    <p>The number is {number}</p>
{:catch error}
    <p style="color: red">{error.message}</p>
{/await}
