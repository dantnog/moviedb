<script>
  import { API, KEY } from '../../lib/api'
  import MovieCard from '../../lib/components/MovieCard.svelte'

  let query = ''
  let media = 'movie'
  let results

  async function load() {
    if (!query || !media) return
    const data = await fetch(
			`${API}/search/${media}${KEY}&page=1&language=en-US&query=${query}`
		).then(res => res.json())
    console.log(data)
    results = (data.results)
  }

  //onMount(() => load())
</script>


<svelte:head>
	<title>Trending - MovieDB</title>
</svelte:head>


<div class="flex align-center my-6 space-x-4">
  <h2 class="text-2xl">Search</h2>
  <select name="media" id="media" bind:value={media} on:change={load}  class="bg-gray-200 dark:bg-gray-800 rounded-md px-2 py-1">
    <option value="movie" class="">Movies</option>
    <option value="tv" class="">Tv Shows</option>
    <option value="person" class="">Person</option>
  </select>
  <form on:submit|preventDefault={load} class="">
    <input type="text" class="px-2 py-1 bg-gray-200 dark:bg-gray-800 focus:ring-2 ring-offset-2 
      ring-offset-white placeholder:italic dark:ring-offset-gray-900 ring-blue-500/50 rounded-md outline-none"
      placeholder="Search..." bind:value={query}
    >
  </form>
</div>


{#if results}
  <div class="grid grid-cols-2 sm:grid-cols-4 lg:grid-cols-6 gap-4 mb-6">
    {#each results as show (show.id)}
      <MovieCard item={show} media={media} />
    {/each}
  </div>
{:else} 
  <h2 class="m-auto text-2xl">Waiting for search...</h2>
{/if}