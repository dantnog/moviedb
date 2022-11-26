<script>
  import { page } from '$app/stores'
	import { onMount } from 'svelte'
  import { API, KEY } from '../../../lib/api'

  const id = $page.url.pathname.split('/')[2]

  let tv

  async function load() {
    tv = await fetch(
			`${API}/tv/${id}${KEY}&language=en-US`
		).then(res => res.json())
    console.log(tv)
  }

  onMount(() => load())
</script>


{#if tv}
<section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-6 mx-auto my-6">
  <div class="lg:col-span-3">
    <img src={`https://image.tmdb.org/t/p/original${tv.backdrop_path}`} alt="Poster" class="rounded-md">
    <h2 class="text-3xl font-semibold text-blue-500/80 my-4">
      {tv.name}<span class="ml-4 text-yellow-500 text-2xl">&#9733;{tv.vote_average.toFixed(1)}</span>
    </h2>
    {#if tv.homepage}
    <a href={tv.homepage} class="bg-green-400 font-bold text-gray-800 px-4 rounded-md">
      HOMEPAGE
    </a>
    {/if}
    <p class="my-4">{tv.overview}</p>

    <div class="grid grid-cols-3 gap-4 lg:gap-6 lg:grid-cols-4">
    {#each tv.seasons as s}
      <div class="rounded-lg overflow-hidden">
        <img src={`https://image.tmdb.org/t/p/w500${s.poster_path}`} alt="Season Poster" class="">
        <div class="p-2">
          <h4 class="font-semibold truncate ">
            {s.name}
          </h4>
          <p class="truncate">
            {s.episode_count} episodes
          </p>
        </div>
      </div>
    {/each}
    </div>
  </div>

  <div class="lg:col-span-2">
    <table class="table-fixed">
      <tbody class="text-left">
        <tr class="border-b-8 border-transparent">
          <th class="w-32">
            Companies
          </th>
          <td class="">
          { tv.production_companies.map(item => item.name).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Created By
          </th>
          <td class="">
          { tv.created_by.map(item => item.name).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Origin Countries
          </th>
          <td class="">
          { tv.origin_country.map(item => item).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Countries
          </th>
          <td class="">
          { tv.production_countries.map(item => item.name).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Spoken Languages
          </th>
          <td class="">
          { tv.spoken_languages?.map(item => item.name).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Genres
          </th>
          <td class="">
          { tv.genres.map(item => item.name).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            First Air Date
          </th>
          <td class="">
            {tv.first_air_date}
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Last Air Date
          </th>
          <td class="">
            {tv.last_air_date}
          </td>
        </tr>


        <tr class="border-y-8 border-transparent">
          <th class="">
            Episodes
          </th>
          <td class="">
            {tv.number_of_episodes}
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Seasons
          </th>
          <td class="">
            {tv.number_of_seasons}
          </td>
        </tr>
        
        <tr class="border-y-8 border-transparent">
          <th class="">
            Runtime
          </th>
          <td class="">
            {tv.episode_run_time[0]} minutes
          </td>
        </tr>

        <tr class="border-t-8 border-transparent">
          <th class="">
            Vote Count
          </th>
          <td class="">
            {tv.vote_count}
          </td>
        </tr>

      </tbody>
    </table>
  </div>

</section>

{:else}
<h2 class="m-auto text-2xl">Loading</h2>
{/if}