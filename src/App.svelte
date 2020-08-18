<script>
  import { fly } from 'svelte/transition';

  import { fetchStore } from './stores/store.js';

  const todos = fetchStore();
  todos.get('http://localhost:1337/todos/');

  import { onMount } from 'svelte';

  onMount(() => {});

  import ProgressCircle from 'svelte-progresscircle';
  import TodoItem from './components/TodoItem.svelte';

  let isHidden = true;
  let value = 70;
  let width;
  $: sidebar = width >= 768;
</script>

<style>
  .progress {
    --progress-color: #48bb78;
    --progress-trackcolor: #cbdfe0;
  }

  span {
    font-size: 1.25rem;
    left: 50%;
    position: absolute;
    top: 50%;
    transform: translate(-50%, -50%);
  }
</style>

<svelte:window bind:innerWidth={width} />
<div class="flex flex-row flex-wrap relative">

  <!-- begin mobile nav -->
  <div class="px-6 py-2 z-20 shadow-lg w-full md:hidden">
    <button on:click={() => (isHidden = !isHidden)}>
      <i class="fa fa-2x fa-bars text-gray-600" />
    </button>
  </div>
  <!-- end mobile nav -->

  <!-- begin sidebar -->
  {#if !isHidden || sidebar}
    <div
      transition:fly|local={{ y: -300, duration: 300 }}
      class="p-2 z-10 mt-10 bg-white shadow-2xl w-full md:block md:mt-0 md:w-84
      fixed md:h-screen">
      <!-- begin inner-column -->
      <div class="flex flex-col bg-white">
        <!-- Begin Avatar -->
        <div class="p-4 w-full">
          <div class="h-full flex items-center shadow p-2 rounded-lg">
            <img
              alt="team"
              class="w-16 h-16 object-cover object-center flex-shrink-0
              rounded-full mr-4"
              src="https://randomuser.me/api/portraits/women/79.jpg" />
            <div class="flex-grow">
              <h2 class="text-gray-700 font-medium text-lg">Hello, User!</h2>
              <p class="text-gray-500">My Account | Log Out</p>
            </div>
          </div>
        </div>
        <!-- End Avatar -->

        <div class="p-4 w-full">
          <div class="h-full text-center shadow rounded-lg p-2">
            <h4 class="text-gray-700 font-medium">Date of Move</h4>
            <h1 class="text-gray-700 font-extrabold text-4xl">9/20/20</h1>
          </div>
        </div>

        <div class="p-4 w-full">
          <div class="progress h-48 py-2 text-center shadow rounded-lg p2">
            <ProgressCircle max="100" {value}>
              <span class="leading-none">
                <p class="text-gray-700 font-extrabold text-4xl">{value}%</p>
                <p class="text-base text-gray-500">complete</p>
              </span>
            </ProgressCircle>
          </div>
        </div>

        <div class="p-4 w-full">
          <div
            class="w-full h-full shadow-md rounded-lg text-gray-700 divide-y
            divide-gray-300">

            <div class="flex items-center justify-between h-12 px-2">
              <p>Overdue Tasks</p>
              <div
                class="h-8 w-8 text-white font-bold bg-red-500 rounded-full flex
                justify-center items-center">
                0
              </div>
            </div>
            <div class="flex items-center justify-between h-12 px-2">
              <p>Due this Week</p>
              <div
                class="h-8 w-8 text-white font-bold bg-orange-500 rounded-full
                flex justify-center items-center">
                0
              </div>
            </div>
            <div class="flex items-center justify-between h-12 px-2">
              <p>Completed Tasks</p>
              <div
                class="h-8 w-8 text-white font-bold bg-green-500 rounded-full
                flex justify-center items-center">
                0
              </div>
            </div>

          </div>
        </div>

      </div>
    </div>
  {/if}

  <main class="w-full md:ml-84 p-6">

    <div class="container mx-auto">

      <div
        class="text-3xl text-gray-700 font-medium leading-relaxed tracking-tight">
        My Checklist
      </div>

      <div class="bg-white shadow-lg p-3 mt-2 flex rounded-lg">
        <div class="flex p-2 items-center">
          <i class="fa fa-2x fa-plus-circle text-gray-200" />
        </div>
        <input
          class="w-full rounded p-2"
          type="text"
          placeholder="What do you have to do?" />
        <button
          class="bg-red-400 hover:bg-red-500 rounded-lg text-white p-2 pl-4 pr-4">
          <p class="font-semibold text-lg">Add</p>
        </button>
      </div>

      <ul class="flex flex-col bg-white py-4 mt-6">
        {#each $todos as todo}
          <TodoItem {...todo} />
        {/each}

      </ul>

      {#each $todos as todo}
         <pre>{JSON.stringify(todo, null, 2)}</pre>
      {/each}

    </div>

  </main>
</div>
