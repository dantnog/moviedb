<script>
  import A from "../components/A.svelte";
  import Theme from "../components/Theme.svelte";
</script>

<div class="bg-gray-100 dark:bg-gray-800 h-12 flex justify-between place-items-center px-4 sm:px-6">
  <h1 class="text-2xl">MovieDB</h1>

  <nav class="">
    <A props={{name: "Home", link:"/"}} />
    <A props={{name: "Best", link:"/"}} />
    <Theme />
  </nav>
</div>