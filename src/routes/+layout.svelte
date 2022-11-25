<script>
  import '../app.css';
  import Header from '../lib/layouts/Header.svelte';
</script>

<div class="">
	<Header />

	<main class="px-4">
		<slot />
	</main>

	<footer>
	</footer>
</div>