<script>
    export let name = ""; // Card name passed as a prop
    let cardImage = ""; // Image URL
    let isVisible = false; // State for visibility
    let containerRef; // Reference to the container

    // Fetch card image only once
    async function fetchCardImage() {
      if (!cardImage) {
        try {
          const response = await fetch(
            `https://api.scryfall.com/cards/named?exact=${encodeURIComponent(name)}`, {
                method: "GET",
                headers:{
                    "Accept":"application/json"
                }
            }
          );
          const data = await response.json();
          cardImage = data.image_uris?.normal || "";
        } catch (error) {
          console.error("Error fetching card image:", error);
        }
      }
    }
  
    // Toggle visibility
    function toggleVisibility() {
      isVisible = !isVisible;
      if (isVisible) fetchCardImage();
    }
  
    // Close tooltip on clicks outside
    function handleClickOutside(event) {
      if (containerRef && !containerRef.contains(event.target)) {
        isVisible = false;
      }
    }
  
    // Add and remove event listener
    import { onMount, onDestroy } from "svelte";
  
    onMount(() => {
      window.addEventListener("click", handleClickOutside);
        return () => {
            window.removeEventListener("click", handleClickOutside);
        }
    
    });
  </script>
  
  <div
    bind:this={containerRef}
    class="relative inline-block focus:outline-none"
    role="button"
    tabindex="0"
    aria-haspopup="true"
    aria-expanded={isVisible}
    aria-label={`Show image of ${name}`}      
    on:mouseleave={() => isVisible = false}           
    on:click={toggleVisibility}     
    on:touchstart={toggleVisibility}                              
    on:keydown={(e) => (e.key === "Enter" || e.key === " ") && toggleVisibility()}
  >
    <div class='text-center'>
        <span class="text-blue-300 underline cursor-pointer">{name}</span>
    </div>
    {#if isVisible && cardImage}
      <div
        class="absolute top-0 left-1/2 transform -translate-x-1/2 mt-2 w-48 bg-white border border-gray-300 rounded shadow-lg z-50"
        role="tooltip"
        aria-label={`Image of ${name}`}
      >
        <img src={cardImage} alt={`Card: ${name}`} class="w-48 h-auto rounded" />
      </div>
    {/if}
  </div>
  <!-- on:mouseenter={() => { isVisible = true; fetchCardImage(); }}
  on:mouseleave={() => isVisible = false}     -->

  <style>
    span {
        user-select: none
    }
  </style>