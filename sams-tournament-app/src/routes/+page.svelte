<script>
    import Formatrules from "$lib/components/formatrules.svelte"
    import Potluck from "$lib/components/potluck.svelte"
    import Points from "$lib/components/points.svelte"
    import Score from "$lib/components/score.svelte"
    import { onMount } from "svelte";
    import Tab from "$lib/components/tab.svelte";
    import Tabs from "$lib/components/tabs.svelte";
    import { json } from "@sveltejs/kit";
    import GroupPhoto from "$lib/components/groupphoto.svelte";

    const lutonFestFiles = import.meta.glob('$lib/tournaments/lutonfest/*.json')
    let lutonFestData = []
    let activeTab = 1

    function setActiveTab(index) {
        console.log("active tab", index)
        activeTab = index;
    }

    async function loadData(){
        // Collect all promises
        const promises = Object.entries(lutonFestFiles).map(([path, resolver]) =>
        resolver().then((module) => {
            return module.default; // Return the JSON data
        })
        );

        // Wait for all promises to resolve
        lutonFestData = await Promise.all(promises);
    }

    onMount(async ()=>{
        await loadData()
        let activeTab = lutonFestData.length -1
    })
</script>

<div class="w-full h-full bg-gray-900">
    <h1 class="bg-gray-800 text-gray-200 text-center">LutonFest</h1>
    <h2 class="bg-gray-700 text-gray-200 text-center">TBD 2026</h2>
    <h2 class="bg-gray-700 text-gray-200 text-center">3 Format Invitational - Sam's Choice, Defending Champion's Choice, and Letter</h2>
    <h2 class="bg-gray-700 text-gray-200 text-center">Start Time: 11:00 AM</h2>
    <h2 class="bg-gray-600 text-gray-200 text-center">Entry: $10 or 3 packs of any MTG Set and a Potluck dish</h2>
    <h2 class="bg-gray-600 text-gray-200 text-center">Additional Fees/Requirements may apply depending on Format</h2>
    <h2 class="bg-gray-600 text-gray-200 text-center">You must bring all decks and required materials or your spot will be given to an alternate, on day of tournament.</h2>
    <h2 class="bg-gray-600 text-gray-200 text-center">Cards can be borrowed from Sam's Collection at a First Come/First Serve Basis</h2>
    <h2 class="bg-gray-500 text-gray-200 text-center">3 Matches of each Format are played using a pairing system.</h2>
    <h2 class="bg-gray-500 text-gray-200 text-center">Points are awarded based on W/L ratio in each format.</h2>
    <h2 class="bg-gray-500 text-gray-200 text-center">Winner is player with most points from all formats.</h2>
    <h2 class="bg-gray-500 text-gray-200 text-center">Winner will become the new Defending Champion and selects 1 format for next year.</h2>
    <Points/>
    <Tabs>
        <div slot="tab-titles" class="bg-gray-800">
            {#each lutonFestData as item, index}
                <Tab title={`LutonFest ${item.year}`} {activeTab} index={index} setActiveTab={()=>{
                    setActiveTab(index)
                }}/>
            {/each}
        </div>

        <div slot="tab-content">
            {#each lutonFestData as item, index}
                {#if index === activeTab}
                    {#each Object.keys(item.formats) as format}
                        <Formatrules rules={item.formats[format]} players={item.players} />
                    {/each}
                    <Score players={item.players} formats={item.formats} />
                    <Potluck players={item.players} />
                    <GroupPhoto photo={item.photo}/>
                {/if}
            {/each}
        </div>
    </Tabs>

</div>
<style>
    h1 {
        text-align: center;
        font-size: 4vh;
    }
</style>