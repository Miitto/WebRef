<script lang="ts">
    import Modal from "../../../Modal.svelte";

    let show: boolean = false;

    export let required = false;

    export let books = [];

    $: filtered = books.filter((book) =>
        book.title.toLowerCase().includes(bookSearch.toLowerCase())
    );

    let value = "";

    let bookSearch = "";

    $: book = books.find((book) => book.id === value);

    $: show && (bookSearch = "");
</script>

<Modal bind:show>
    <h2 slot="header">Select Book</h2>
    <form>
        <input
            type="text"
            placeholder="Search for a book..."
            bind:value={bookSearch}
        />
    </form>
    {#each filtered as book (book.id)}
        <button
            on:click|preventDefault={() => {
                value = book.id;
                show = false;
            }}
        >
            <h3>{book.title}</h3>
        </button>
    {:else}
        <p>No Books Found</p>
    {/each}
</Modal>
<input
    type="text"
    {required}
    placeholder="Select a book..."
    on:click|preventDefault={() => (show = true)}
    value={book?.title ?? ""}
    on:keydown={(evt) => {
        if (evt.key != "Tab" && evt.key != "Escape") show = true;
    }}
/>
<input
    type="text"
    name="book"
    hidden
    bind:value
/>

<style lang="scss">
    button {
        background-color: #5555;
        backdrop-filter: blur(10px);
        text-align: left;
    }
</style>
