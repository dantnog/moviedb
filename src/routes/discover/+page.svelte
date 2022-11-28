<script>
  import { onMount } from 'svelte';
  import { API, KEY } from '../../lib/api'
  import MovieCard from '../../lib/components/MovieCard.svelte'

  let media = 'movie'
  let sort_by = 'popularity.desc'

  let results

  async function load() {
    let query = `${API}/discover/${media}/${KEY}&sort_by=${sort_by}&page=1&language=en-US`
    const data = await fetch(
			query
		).then(res => res.json())
    results = data.results
    console.log(results)
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
