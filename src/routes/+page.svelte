<script>
	import { onMount } from 'svelte'
  import { API, KEY } from '../lib/api'
  import MovieCard from '../lib/components/MovieCard.svelte'

  let trending
  let media = 'movie'
  let time = 'week'

  async function load() {
    const data = await fetch(
			`${API}/trending/${media}/${time}${KEY}&page=1&language=en-US`
		).then(res => res.json())
    trending = data.results
  }

  onMount(() => load())
</script>

<svelte:head>
	<title>Trending - MovieDB</title>
</svelte:head>


<div class="flex align-center my-6 space-x-4">
  <h2 class="text-2xl">Trending</h2>
  <select name="media" id="media" bind:value={media} on:change={load}  class="bg-gray-200 dark:bg-gray-800 rounded-md px-2 py-1">
    <option value="movie" class="">Movies</option>
    <option value="tv" class="">Tv Shows</option>
    <option value="person" class="">Person</option>
    <option value="all" class="">All</option>
  </select>
  <select name="time" id="time"  bind:value={time} on:change={load} class="bg-gray-200 dark:bg-gray-800 rounded-md px-2 py-1">
    <option value="week" class="">Week</option>
    <option value="day" class="">Day</option>
  </select>
</div>


{#if trending}
  <div class="grid grid-cols-2 sm:grid-cols-4 lg:grid-cols-6 gap-4 mb-6">
    {#each trending as show (show.id)}
      <MovieCard item={show} />
    {/each}
  </div>
{:else} 
  <h2 class="m-auto text-2xl">Loading...</h2>
{/if}