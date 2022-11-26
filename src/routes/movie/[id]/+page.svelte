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
<section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-6 mx-auto my-6">
  <div class="lg:col-span-3">
    <img src={`https://image.tmdb.org/t/p/original${movie.backdrop_path}`} alt="Poster" class="rounded-md">
    <h2 class="text-3xl font-semibold text-blue-500/80 my-4">
      {movie.title}<span class="ml-4 text-yellow-500 text-2xl">&#9733;{movie.vote_average.toFixed(1)}</span>
    </h2>
    <a href={`https://www.imdb.com/title/${movie.imdb_id}`} class="bg-yellow-400 text-gray-800 font-bold px-4 rounded-md">
      IMDb
    </a>
    {#if movie.homepage}
    <a href={movie.homepage} class="bg-green-400 font-bold text-gray-800 px-4 rounded-md">
      HOMEPAGE
    </a>
    {/if}
    <p class="my-4">{movie.overview}</p>
  </div>

  <div class="lg:col-span-2">
    <table class="table-fixed">
      <tbody class="text-left">
        <tr class="border-b-8 border-transparent">
          <th class="w-32">
            Companies
          </th>
          <td class="">
          { movie.production_companies.map(item => item.name).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Countries
          </th>
          <td class="">
          { movie.production_countries.map(item => item.name).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Spoken Languages
          </th>
          <td class="">
          { movie.spoken_languages?.map(item => item.name).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Genres
          </th>
          <td class="">
          { movie.genres.map(item => item.name).join(', ') }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Release Date
          </th>
          <td class="">
            {movie.release_date}
          </td>
        </tr>
        
        <tr class="border-y-8 border-transparent">
          <th class="">
            Runtime
          </th>
          <td class="">
            {movie.runtime} minutes
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Budget
          </th>
          <td class="">
            R${movie.budget.toFixed(2)}
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Revenue
          </th>
          <td class="">
            R${movie.revenue.toFixed(2)}
          </td>
        </tr>

        <tr class="border-t-8 border-transparent">
          <th class="">
            Vote Count
          </th>
          <td class="">
            {movie.vote_count}
          </td>
        </tr>

      </tbody>
    </table>
  </div>
</section>

{:else}
<h2 class="m-auto text-2xl">Loading</h2>
{/if}