<script>
  import { page } from '$app/stores'
	import { onMount } from 'svelte'
  import { API, KEY } from '../../../lib/api'

  const id = $page.url.pathname.split('/')[2]

  let person

  async function load() {
    person = await fetch(
			`${API}/person/${id}${KEY}&language=en-US`
		).then(res => res.json())
    console.log(person)
  }

  onMount(() => load())
</script>


{#if person}
<section class="grid grid-cols-1 sm:grid-cols-3 gap-4 lg:gap-6 my-6">
  <div class="w-[55%] mx-auto sm:w-auto">
    <img src={`https://image.tmdb.org/t/p/original${person.profile_path}`} alt="Poster" class="rounded-md">
  </div>

  <div class="sm:col-span-2">
    <h2 class="text-3xl font-semibold text-blue-500/80 mb-4">
      {person.name}
    </h2>
    <a href={`https://www.imdb.com/name/${person.imdb_id}`} class="bg-yellow-400 text-gray-800 font-bold px-4 rounded-md">
      IMDb
    </a>
    {#if person.homepage}
    <a href={person.homepage} class="bg-green-400 font-bold text-gray-800 px-4 rounded-md">
      HOMEPAGE
    </a>
    {/if}
    <p class="my-4">{person.biography}</p>

    <table class="table-fixed">
      <tbody class="text-left">
        <tr class="border-b-8 border-transparent">
          <th class=" w-32">
            Place of birth
          </th>
          <td class="">
          { person.place_of_birth }
          </td>
        </tr>

        <tr class="border-y-8 border-transparent">
          <th class="">
            Birthday
          </th>
          <td class="">
            {person.birthday}
          </td>
        </tr>
        
        {#if person.deathday}
        <tr class="border-t-8 border-transparent">
          <th class="">
            Birthday
          </th>
          <td class="">
            {person.birthday}
          </td>
        </tr>
        {/if}

      </tbody>
    </table>
  </div>
</section>

{:else}
<h2 class="m-auto text-2xl">Loading</h2>
{/if}