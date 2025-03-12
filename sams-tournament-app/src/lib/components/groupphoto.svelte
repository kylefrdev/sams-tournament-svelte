<script>
    export let photo
    const imgURL = new URL("$lib/assets/"+photo, import.meta.url).href
</script>

<!-- <img alt="winner.jpg" src="{imgURL}"> -->
 <img alt={photo} src={`/images/${photo}`}>

<style>
    img {
        width:100%;
        height:100%;
    }
</style>