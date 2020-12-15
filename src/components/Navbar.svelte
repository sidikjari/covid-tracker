<script>
  import { slide } from 'svelte/transition';
  
  let isShow = false;
  const navHandler = () => isShow = !isShow;
  
</script>

<nav class="w-full flex z-40 fixed mt-0 top-0 justify-between bg-teal-500 p-4">
  <div class="flex items-center flex-shrink-0 text-white mr-6">
    <span class="font-semibold text-xl tracking-tight">
      <i class="fa fa-map" aria-hidden="true"></i>
      Covid Tracker
    </span>
  </div>
  <div>
    <a class="no-underline" href="https://github.com/sidik-jari/svelte-covid-tracker.git">
      <i class="fa fa-github fa-2x text-white" aria-hidden="true"></i>
    </a>
  </div>
</nav>
