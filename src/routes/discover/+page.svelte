<script>
  import { onMount } from 'svelte';
  import { API, KEY } from '../../lib/api'
  import MovieCard from '../../lib/components/MovieCard.svelte'

  let media = 'movie'
  let sort_by = 'popularity.desc'
  let page = 1
  let pages = []

  let results

  function changePage(step) {
    page += step
    if (page < 1 || page > 1000) {
      page += -step
      return
    }
    load()
  }

  function selectPage(num) {
    if (num == page) return
    if (num < 1 || num > 1000) return
    page = num
    load()
  }

  function preparePages() {
    let count = page - 5
    let newpages = []
    while (newpages.length < 11) {
      if (count > 0 && count < 1000) {
        newpages.push(count)
      }
      count += 1
    }
    pages = newpages
  }

  async function load() {
    preparePages()
    let query = `${API}/discover/${media}${KEY}&sort_by=${sort_by}&page=${page}&language=en-US`
    const data = await fetch(
			query
		).then(res => res.json())
    results = data.results
    console.log(query)
  }

  onMount(() => load())
</script>


<svelte:head>
	<title>Discover - MovieDB</title>
</svelte:head>



<div class="flex align-center my-6 space-x-4">
  <h2 class="text-2xl">Discover</h2>
  <select name="media" id="media" bind:value={media} on:change={load}  class="bg-gray-200 dark:bg-gray-800 rounded-md px-2 py-1">
    <option value="movie" class="">Movies</option>
    <option value="tv" class="">Tv Shows</option>
  </select>
  <select name="time" id="time"  bind:value={sort_by} on:change={load} class="bg-gray-200 dark:bg-gray-800 rounded-md px-2 py-1">
    <option value="popularity.desc" class="">Most popular</option>
    <option value="popularity.asc" class="">Least popular</option>
    <option value="release_date.desc" class="">Newest</option>
    <option value="release_date.asc" class="">Oldest</option>
    <option value="vote_average.desc" class="">Highest score</option>
    <option value="vote_average.asc" class="">Lowest score</option>
  </select>
</div>


{#if results}
  <div class="grid grid-cols-2 sm:grid-cols-4 lg:grid-cols-6 gap-4 mb-6">
    {#each results as show (show.id)}
      <MovieCard item={show} media={media}/>
    {/each}
  </div>
{:else} 
  <h2 class="m-auto text-2xl">Loading...</h2>
{/if}

<div class="flex justify-center mb-6">
  <div class="overflow-hidden rounded-md space-x-0">
    <button on:click={() => changePage(-1)} class="px-4 h-10 bg-gray-200 dark:bg-gray-800 hover:bg-gray-300 hover:dark:bg-gray-700">
      Prev
    </button>
    {#each pages as pag (pag)}
    <button on:click={() => selectPage(pag)} 
      class="w-10 h-10 
      {pag === page ? "bg-blue-500/80" : "bg-gray-200 dark:bg-gray-800 hover:bg-gray-300 hover:dark:bg-gray-700"}"
    >
      {pag}
    </button>
    {/each}
    <button on:click={() => changePage(1)} class="px-4 h-10 bg-gray-200 dark:bg-gray-800 hover:bg-gray-300 hover:dark:bg-gray-700">
      Next
    </button>
  </div>
</div>