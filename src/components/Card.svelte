<script>
  export let title;
  export let value;
  export let bg_color;
  export let img;
</script>

<div class="max-w-sm z-0 flex items-center justify-center rounded overflow-hidden relative {bg_color} shadow-lg p-3">
  <img class="w-64 h-64 absolute m-auto opacity-25" src="{img}" alt="coronavirus">
  <div class="flex px-6 py-4">
    <div class="font-bold text-xl text-white text-center mb-2 z-40">
      <h1>{title}</h1>
      <h1>
        {@html value}
      </h1>
    </div>
  </div>
</div>
