<script>
    import Card from "./card.svelte";
    import Collapsible from "./collapsible.svelte";

    export let title
    export let list = []
</script>

<Collapsible>
    <h1 class="bg-gray-800 text-gray-200" name="header" slot="header">{title}</h1>
    <div class="grid grid-cols-3 gap-2" slot="content">
        {#each list as card}
            <Card name={card}></Card>
        {/each}
    </div>
</Collapsible>

<style>
    h1 {
        text-align: center;
    }
</style>