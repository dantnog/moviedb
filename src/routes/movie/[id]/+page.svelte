<script>
  import { page } from '$app/stores'
	import { onMount } from 'svelte'
  import { API, KEY } from '../../../lib/api'

  const id = $page.url.pathname.split('/')[2]

  let movie

  async function load() {
    movie = await fetch(
			`${API}/movie/${id}${KEY}&language=en-US`
		).then(res => res.json())
  }

  onMount(() => load())
</script>


{#if movie}
<section class="max-w-xl mx-auto my-6">
  <img src={`https://image.tmdb.org/t/p/original${movie.backdrop_path}`} alt="Poster" class="rounded-md">
  <h2 class="text-3xl font-semibold text-blue-500/80 my-4">
    {movie.title}
  </h2>
  <p class="my-4">{movie.overview}</p>

  <table class="table-fixed">
    <tbody class="">
      <tr class="">
        <th class="text-left w-32">
          Companies
        </th>
        <td class="">
        { movie.production_companies.map(item => item.name).join(', ') }
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Countries
        </th>
        <td class="">
        { movie.production_countries.map(item => item.name).join(', ') }
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Genres
        </th>
        <td class="">
        { movie.genres.map(item => item.name).join(', ') }
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Release Date
        </th>
        <td class="">
          {movie.release_date}
        </td>
      </tr>
      
      <tr class="text-left">
        <th class="">
          Runtime
        </th>
        <td class="">
          {movie.runtime} minutes
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Budget
        </th>
        <td class="">
          R${movie.budget.toFixed(2)}
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Revenue
        </th>
        <td class="">
          R${movie.revenue.toFixed(2)}
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Vote Average
        </th>
        <td class="">
          {movie.vote_average.toFixed(1)}
        </td>
      </tr>

      <tr class="text-left">
        <th class="">
          Vote Count
        </th>
        <td class="">
          {movie.vote_count}
        </td>
      </tr>

    </tbody>
  </table>

</section>

{:else}
<h2 class="m-auto text-2xl">Loading</h2>
{/if}