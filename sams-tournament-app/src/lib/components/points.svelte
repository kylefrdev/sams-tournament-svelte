<script>
    import Collapsible from "./collapsible.svelte";

    let points = [
        [0,3,0,0],
        [0,2,1,1],
        [0,1,2,1],
        [0,0,3,1],
        [1,2,0,1],
        [1,1,1,2],
        [1,0,2,3],
        [2,1,0,3],
        [2,0,1,4],
        [3,0,0,5],
    ]
</script>

<Collapsible>
    <h1 class="bg-gray-800 text-gray-200" name="header" slot="header">W/L/T Ratio - Points Table</h1>
    <h2 class="bg-gray-700 text-gray-200" name="header">If there is a tie between first place, sudden death round is played with agreed upon format</h2>
    <table class="table-auto border-collapse border border-gray-500 w-full bg-gray-700" slot="content">
        <thead class="bg-purple-950">
            <tr>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">W/L/T</th>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Win</th>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Loss</th>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Tie</th>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Points</th>
            </tr>
        </thead>
        <tbody class="bg-purple-900">
            {#each points as point}
                <tr>

                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{`${point[0]}/${point[1]}/${point[2]}`}</td>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{point[0]}</td>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{point[1]}</td>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{point[2]}</td>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{point[3]}</td>
                </tr>
            {/each}
        </tbody>
    </table>
</Collapsible>