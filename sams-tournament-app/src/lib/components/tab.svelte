<script>
    export let title = '';
    export let index = 0;
    export let activeTab = null;
    export let setActiveTab = () => {};
  </script>
  
  <button
    class="tab-title border-2 border-solid {activeTab === index ? 'border-purple-600' : 'border-gray-700'}"
    on:click={setActiveTab}
  >
    {title}
  </button>

  <style>
    .tab-title {
        font-size:3vh;
        cursor: pointer;
        padding-right:5px;
        padding-left: 5px;
    }
  </style>