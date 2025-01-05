<script>
    import Collapsible from "./collapsible.svelte";

    export let players
</script>

<Collapsible>
    <h1 class="bg-gray-800 text-gray-200" name="header" slot="header">Potluck Signup</h1>
    <table class="table-auto border-collapse border border-gray-500 w-full bg-gray-700" slot="content">
        <thead class="bg-purple-950">
            <tr>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Player</th>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-center">Dish</th>
            </tr>
        </thead>
        <tbody class="bg-purple-900">
            {#each Object.keys(players) as player}
                <tr>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{player}</td>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{players[player].potluck}</td>
                </tr>
            {/each}
        </tbody>
    </table>
</Collapsible>