<script>
  export let item;
</script>

<div class="rounded-lg overflow-hidden hover:bg-gray-100 dark:hover:bg-gray-800 group">
  <a href={`/${item.title ? 'movie' : 'tv'}/${item.id}`} class="">
    <div class="overflow-hidden h-68">
      <img src={`https://image.tmdb.org/t/p/w500${item.poster_path}`} alt={item.title || item.name} 
        class="object-cover group-hover:scale-110 transition-all duration-300 ">
    </div>
    <div class="p-2">
      <h4 class="font-semibold group-hover:text-blue-500/80 truncate overflow-hidden">{item.original_title || item.original_name}</h4>
      <div class="flex justify-between">
        <p class="text-sm">{item.release_date || item.first_air_date}</p>
        <span class="text-sm bg-yellow-300 dark:bg-yellow-700 dark:text-gray-200 px-1 rounded-md">{item.vote_average.toFixed(1)}</span>
      </div>
    </div>
  </a>
</div>