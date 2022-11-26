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
<section class="max-w-xl mx-auto my-6">
  <img src={`https://image.tmdb.org/t/p/original${tv.backdrop_path}`} alt="Poster" class="rounded-md">
  <h2 class="text-3xl font-semibold text-blue-500/80 my-4">
    <a href={tv.homepage}>{tv.name}</a>
  </h2>
  <p class="my-4">{tv.overview}</p>

  <table class="table-fixed">
    <tbody class="">
      <tr class="">
        <th class="text-left w-32">
          Companies
        </th>
        <td class="">
        { tv.production_companies.map(item => item.name).join(', ') }
        </td>
      </tr>

      <tr class="">
        <th class="text-left w-32">
          Created By
        </th>
        <td class="">
        { tv.created_by.map(item => item.name).join(', ') }
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Origin Countries
        </th>
        <td class="">
        { tv.origin_country.map(item => item).join(', ') }
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Countries
        </th>
        <td class="">
        { tv.production_countries.map(item => item.name).join(', ') }
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Genres
        </th>
        <td class="">
        { tv.genres.map(item => item.name).join(', ') }
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          First Air Date
        </th>
        <td class="">
          {tv.first_air_date}
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Episodes
        </th>
        <td class="">
          {tv.number_of_episodes}
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Seasons
        </th>
        <td class="">
          {tv.number_of_seasons}
        </td>
      </tr>
      
      <tr class="text-left">
        <th class="">
          Runtime
        </th>
        <td class="">
          {tv.episode_run_time[0]} minutes
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Vote Average
        </th>
        <td class="">
          {tv.vote_average.toFixed(1)}
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Vote Count
        </th>
        <td class="">
          {tv.vote_count}
        </td>
      </tr>

    </tbody>
  </table>

</section>

{:else}
<h2 class="m-auto text-2xl">Loading</h2>
{/if}