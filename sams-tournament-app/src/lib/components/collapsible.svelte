<script>
    export let isOpen = false;

    function toggle() {
        isOpen = !isOpen
    }
</script>


<div class="collapsible border border-gray-700">
    <!-- Button Header -->
    <button
      type="button"
      class="w-full collapsible-header cursor-pointer flex justify-between items-center p-4 bg-gray-800"
      on:click={toggle}
    >
      <slot name="header">Default Header</slot>
      <span class="bg-gray-800 text-gray-200 rounded">
        {isOpen ? "-" : "+"}
      </span>
    </button>
  
    <!-- Collapsible Content -->
    <div
      class="overflow-hidden transition-all duration-300"
      style={`max-height: ${isOpen ? 'auto' : '0px'};`}
    >
      <div>
        <slot name="content">Default Content</slot>
      </div>
    </div>
  </div>

<style>
</style>