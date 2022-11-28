<script>
  import { page } from '$app/stores'
	import { onMount } from 'svelte'
  import { API, KEY } from '../../../../../lib/api'

  const currentPath = $page.url.pathname
    console.log(currentPath)

  let season 

  async function load() {
    season = await fetch(
			`${API}${currentPath}${KEY}&language=en-US`
		).then(res => res.json())
  }

  onMount(() => load())
</script>


<svelte:head>
	<title>{season ? season.name : 'Season'} - MovieDB</title>
</svelte:head>


<section class="">
  SEASON
</section>