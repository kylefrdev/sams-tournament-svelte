<script>
    import Collapsible from "./collapsible.svelte";

    export let players
    export let formats

    let playerResults = Object.values(players).sort((a, b)=>{
        // First, compare by 'place' in ascending order
        if (a.place !== b.place) {
            return a.place - b.place
        }

        // If places are the same, compare by 'name' alphabetically
        return a.name.localeCompare(b.name)
    })

    function getTotal(totalArray){
        var total = 0;
        
        for (var i=0; i<totalArray.length; i++){
            total += +totalArray[i];
        }

        return total
    }
</script>

<!-- {#each Object.keys(players) as player} -->
    <Collapsible>
        <h1 class="bg-gray-800 text-gray-200" name="header" slot="header">Tournament Results</h1>
        <table class="table-auto border-collapse border border-gray-500 w-full bg-gray-700" slot="content">
            <thead class="bg-purple-950">
                <tr>
                    <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Place</th>
                    <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Player</th>
                    {#each Object.keys(formats) as format}
                        <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">{formats[format]?.format}</th>
                    {/each}
                    <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Total Points</th>
                </tr>
            </thead>
            <tbody class="bg-purple-900">
                {#each playerResults as player, i}
                    {#if player.place >0}
                    <tr>
                        <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{player.place}</td>
                        <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{player.name}</td>
                        {#each player.results as playerResults}
                            <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{playerResults}</td>
                        {/each}
                        <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{getTotal(player.results)}</td>
                    </tr>
                    {/if}
                {/each}
            </tbody>
        </table>
    </Collapsible>
<!-- {/each} -->