<script>
    export let activeTab = null; // Active tab index
    export let setActiveTab = () => {}; // Function to update active tab
  </script>

  <div class="tabs bg-gray-700 text-gray-200">
    <div class="tab-titles">
      <slot name="tab-titles" {activeTab} {setActiveTab} />
    </div>
  
    <div class="tab-content">
      <slot name="tab-content" {activeTab} />
    </div>
  </div>
  
  <style>
    .tabs {
      display: flex;
      flex-direction: column;
    }
  
    .tab-titles {
      display: flex;
    }
  </style>