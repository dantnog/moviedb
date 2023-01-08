<script>
  import A from "../components/A.svelte";
  import AH from "../components/AH.svelte";
  import Theme from "../components/Theme.svelte";

  let navHidden = true

  function showNav() {
    if (navHidden) {
      document.getElementById('nav-res').classList.replace('hidden', 'absolute')
    } else {
      document.getElementById('nav-res').classList.replace('absolute', 'hidden')
    }
    navHidden = !navHidden
  }
</script>

<div class="bg-gray-200 dark:bg-gray-800 h-12 flex justify-between place-items-center px-4 sm:px-6">
  <h1 class="text-2xl">MovieDB</h1>

  <nav class="hidden sm:block">
    <A props={{name: "Home", link:"/"}} />
    <A props={{name: "Discover", link:"/discover"}} />
    <A props={{name: "Search", link:"/search"}} />
    <div class="inline-block hover:bg-gray-300 dark:hover:bg-gray-700 rounded-md">
      <Theme />
    </div>
  </nav>

  <nav id="nav-res"
    class="hidden sm:hidden top-12 left-0 sm:h-auto p-3
    sm:w-auto w-full justify-between bg-gray-200 dark:bg-gray-800 "
  >
    <button on:click={showNav} class="text-left w-full">
      <AH props={{name: "Home", link:"/"}} />
    </button>
    <button on:click={showNav} class="text-left w-full">
      <AH props={{name: "Discover", link:"/discover"}} />
    </button>
    <button on:click={showNav} class="text-left w-full">
      <AH props={{name: "Search", link:"/search"}} />
    </button>
    <div on:click={showNav} class="w-full hover:bg-gray-300 dark:hover:bg-gray-700 rounded-md">
      <Theme />
    </div>
  </nav>

  <button 
    on:click={showNav}
    type="button" 
    class="block sm:hidden w-10 h-[80%] hover:bg-gray-300 dark:hover:bg-gray-700 rounded-md"
  >
    {#if navHidden}
      <span class="text-4xl my-4">&#8285;</span>
    {:else}
      <span class="text-3xl">&#9747;</span>
    {/if}
  </button>
</div>