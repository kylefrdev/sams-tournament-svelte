<script>
    import Collapsible from "./collapsible.svelte";

    export let results

    function getTotal(totalArray){
        var total = 0;
        
        for (var i=0; i<totalArray.length; i++){
            total += +totalArray[i];
        }

        return total
    }
</script>

{#each Object.keys(results) as result}
    <Collapsible>
        <h1 class="bg-gray-800 text-gray-200" name="header" slot="header">{result} - Tournament Results</h1>
        <table class="table-auto border-collapse border border-gray-500 w-full bg-gray-700" slot="content">
            <thead class="bg-purple-950">
                <tr>
                    <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Place</th>
                    <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Player</th>
                    {#each results[result].formats as format}
                        <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">{format}</th>
                    {/each}
                    <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Total Points</th>
                </tr>
            </thead>
            <tbody class="bg-purple-900">
                {#each Object.keys(results[result].players) as player, i}
                    <tr>
                        <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{i+1}</td>
                        <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{player}</td>
                        {#each results[result].players[player] as playerResults}
                            <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{playerResults}</td>
                        {/each}
                        <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{getTotal(results[result].players[player])}</td>
                    </tr>
                {/each}
            </tbody>
        </table>
    </Collapsible>
{/each}