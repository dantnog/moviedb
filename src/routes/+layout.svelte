<script>
  import '../app.css';
  import Header from '../lib/layouts/Header.svelte';
	import tmdb from '../lib/images/tmdb.svg'
</script>

<div class="">
	<Header />

	<main class="px-4">
		<slot />
	</main>

	<footer class="h-12 mt-6 bg-gray-100 dark:bg-gray-800 flex justify-center">
		<div class="flex place-items-center space-x-2">
			<p class="">Data fetched from</p>
			<img src={tmdb} alt="The Movie DB" class="h-3">
		</div>
	</footer>
</div>