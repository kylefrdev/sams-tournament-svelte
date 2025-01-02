<script>
    import Collapsible from "./collapsible.svelte";

    export let odds
    export let players

    function renderPlayers(letter) {
        let output = ""
        for(let player of Object.entries(players)) {
            if(player[1].letter == letter){
                if(output == "") {
                    output += player[0]
                } else {
                    output += `, ${player[0]}`
                }
            }
        }
        return output
    }
</script>

<Collapsible>
    <h1 class="bg-gray-800 text-gray-200" name="header" slot="header">Letter Assignments</h1>
    <table class="table-auto border-collapse border border-gray-500 w-full bg-gray-700" slot="content">
        <thead class="bg-purple-950">
            <tr>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-left">Letter</th>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-left">Die Faces</th>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-left">Percentage</th>
                <th class="border border-purple-900 text-gray-200 px-4 py-2 text-left">Players</th>
            </tr>
        </thead>
        <tbody class="bg-purple-900">
            {#each Object.entries(odds) as [key, odd]}
                <tr>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{key}</td>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{odd.faces[0]==odd.faces[1]?odd.faces[0]:`${odd.faces[0]}-${odd.faces[1]}`}</td>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{odd.faces[1]-odd.faces[0]+1}%</td>
                    <td class="border border-purple-800 text-gray-200 px-4 py-2 text-center">{renderPlayers(key)}</td>
                </tr>
            {/each}
        </tbody>
    </table>
</Collapsible>