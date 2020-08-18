<script>
  export let title = 'Task Title';
  export let completed = false;
  export let due_date = '7/30/2020';
  export let link;
</script>

<li class="flex flex-row mb-2 shadow-md rounded-lg">
  <div
    class="bg-white rounded-lg flex flex-1 items-center p-4
    transition duration-500 ease-in-out transform hover:translate-y-1
    hover:shadow-lg">
    {#if completed}
      <div
        class="flex flex-col rounded-full w-12 h-12 bg-green-500 justify-center
        items-center mr-4 cursor-pointer">
        <i class="text-white fa fa-2x fa-check-circle" />
      </div>
      {:else}
      <div
        class="flex flex-col rounded-full w-12 h-12 bg-gray-300 hover:bg-green-300 justify-center
        items-center mr-4 cursor-pointer">
        <i class="text-white fa fa-2x fa-circle" />
      </div>
    {/if}
    <div class="flex-1 pl-1">
      <div class="font-medium text-gray-600">{title}</div>
      {#if link}
        <div class="text-gray-600 text-sm">{link}</div>
      {/if}
    </div>
    <div class="ml-4 text-gray-600 text-sm">{due_date}</div>
    <button class="ml-6">
      <i
        class="fa fa-lg fa-pencil text-orange-500 hover:text-orange-600
        transition duration-150" />
    </button>
    <button class="ml-2">
      <i
        class="fa fa-lg fa-times-circle text-red-500 hover:text-red-600
        transition duration-150" />
    </button>
  </div>
</li>
