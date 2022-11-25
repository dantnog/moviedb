<script>
  let dark = false

  function changeTheme() {
    document.documentElement.classList.toggle('dark')
    dark = !dark
  }
</script>

<button 
  on:click={changeTheme}
  class="ml-2">
  {#if dark === true}
    &#127774;
  {:else}
    &#127770;
  {/if}
</button>