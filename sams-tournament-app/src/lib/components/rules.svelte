<script>
    export let deckRestrictions = null
</script>
    
<style>
    
</style>

<div class="container">
    {#if deckRestrictions != null}
        <h1>{deckRestrictions?.format}</h1>
        <h2>Size Limits</h2>
        <div class="grid grid-cols-2 gap-4">
            <h3>Minimum</h3>
            <h3>{deckRestrictions?.copies}</h3>
            <h3>Maximum</h3>
            <h3>{deckRestrictions?.copies}</h3>
        </div>
        <h2>Copies Per Card</h2>
        <h3>{deckRestrictions?.copies}</h3>
        <h2>Ban List</h2>
        {#each deckRestrictions.bans as ban}
            <h2>{ban?.name}</h2>
        {/each}
        <h2>Restricted List</h2>
        {#each deckRestrictions.restricted as restrict}
            <div class="grid grid-cols-2 gap-4">
                <h2>{restrict?.name}</h2>
                <h2>{restrict?.limit}</h2>
            </div>
        {/each}
    {/if}
    {#if deckRestrictions.clarifications != null} 
        <h1>Rules Clarifications</h1>
    {/if}
</div>