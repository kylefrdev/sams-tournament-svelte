<script>
    import Bans from "./bans.svelte";
    import Odds from "./odds.svelte"
    import Collapsible from "./collapsible.svelte";
    export let rules
    export let players
</script>

{#if rules}
    <Collapsible>
        <h1 class="bg-gray-800 text-gray-200" slot="header">{rules.title} - {rules.format}</h1>
        <div class=' border border-purple-800' slot="content">
            <h1 class="bg-gray-800 text-gray-200">Format</h1>
            <h1 class="bg-gray-700 text-gray-200 text-2xl">{rules.format}</h1>
            <div class="grid grid-cols-2">
                <h2 class="bg-gray-800 text-gray-200">Base Rules</h2>
                <h2 class="bg-gray-800 text-gray-200">Copies per Card</h2>
                <h3 class="bg-gray-700 text-gray-200 text-2xl">{rules.base_rules}</h3>
                <h3 class="bg-gray-700 text-gray-200 text-2xl">{rules.copies ?? "\u221E"}</h3>
            </div>
            <h2 class="bg-gray-800 text-gray-200">Deck Size Limits</h2>
            <div class="grid grid-cols-2">
                <h2 class="bg-gray-700 text-gray-200">Min</h2>
                <h2 class="bg-gray-700 text-gray-200">Max</h2>
                <h2 class="bg-gray-600 text-gray-200 text-2xl">{rules.min}</h2>
                <h2 class="bg-gray-600 text-gray-200 text-2xl">{rules.max ?? "\u221E"}</h2>
            </div>
            <h1 class="bg-gray-800 text-gray-200">Format Rules</h1>
            {#each rules.rules as rule}
                <p class="bg-gray-700 text-gray-200 border-b border-gray-800">{rule}</p>
            {/each}
            <h1 class="bg-gray-800 text-gray-200">Rules Clarifications</h1>
            {#each rules.clarifications as clarification}
                <p class="bg-gray-700 text-gray-200 border-b border-gray-800">{clarification}</p>
            {/each}
            <Bans title="Ban List" list={rules.bans}/>
            <Bans title="Sam's Ban List" list={rules.sams_bans}/>
            <Bans title="Restricted List" list={rules.restricted}/>
            {#if rules?.odds}
                <Odds odds={rules.odds} players={players}/>
            {/if}
        </div>
    </Collapsible>
{:else}
    <div>
        <h1>Missing Format</h1>
    </div>
{/if}


<style>
    h1, h2, h3 {
        text-align: center;
    }

    p {
        text-align: center;
    }
</style>