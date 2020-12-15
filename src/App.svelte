<script>
  import { onMount } from 'svelte';
  import Navbar from './components/Navbar.svelte';
  import Card from './components/Card.svelte';
  import { DATA } from './resource/resource.js';

  let cards = [
    {title: 'Positive', img: '/img/virus.png', bg_color: 'bg-blue-600'},
    {title: 'Deaths', img: '/img/skull.png', bg_color: 'bg-red-600'},
    {title: 'Recovered', img: '/img/injection.png', bg_color: 'bg-green-600'},
  ];
  let spinner = '<i class="fa fa-spinner fa-spin" aria-hidden="true"></i>';
  
  async function getData(d){
    try {
  	   let res = await fetch(DATA.CORS+d);
  	   return await res.json();
    }catch(err){
  	   throw err;
    }
  }
  
  let global = [];
  let indonesia = [];
  let country = [];
  onMount(async () => {
    try {
      let res_indonesia = await getData(DATA.INDO_PROV);
      let res_country = await getData(DATA.COUNTRY);
      let res_global = await Promise.all([getData(DATA.GLOBAL.POSITIVE), getData(DATA.GLOBAL.DEATH), getData(DATA.GLOBAL.RECOVERED)]);
      global = res_global.map((data, i)=> {
        let obj = {
          title: cards[i].title,
          img: cards[i].img,
          bg_color: cards[i].bg_color
        }
        return Object.assign(data, obj);
      });
      indonesia = res_indonesia;
      country = res_country;
    }catch(err){
      throw err;
    }
  })
  
</script>

<Navbar />
<main class="mt-20">
  <h1 class="text-center font-bold text-3xl mt-3"> Covid Tracker </h1>
  <p class="text-center m-2">#staysafe #stokindomie #dirumahaja #staysantuy #gaksengaja</p>
  <div class="block">
    <h2 class="text-center text-2xl my-2"> Data Global </h2>
  </div>
  
  <div class="md:flex md:w-full md:justify-between md:items-center">
    {#each global as {title, value, img, bg_color}}
      <div class="m-2 md:flex-1 shadow-lg">
        <Card {title} {value} {img} {bg_color} />
      </div>
      {:else}
        {#each cards as {title, img, bg_color}}
        <div class="m-2 md:flex-1 shadow-lg">
          <Card {title} value={spinner} {img} {bg_color} />
        </div>
        {/each}
    {/each}
  </div>
  
  <div class="w-full sm:block md:flex md:justify-center md:items-center mt-2">
    <div class="p-3">
    <h1 class="text-center text-2xl"> Indonesia Province </h1>
    <div class="md:block overflow-auto my-3" style="height:30vh;">
      <table class="table-auto">
        <thead>
          <tr>
            <th class="border border-black px-4 py-2">No</th>
            <th class="border border-black px-4 py-2">Province</th>
            <th class="border border-black px-4 py-2">Positive</th>
            <th class="border border-black px-4 py-2">Deaths</th>
            <th class="border border-black px-4 py-2">Recovered</th>
          </tr>
        </thead>
        <tbody>
        {#each indonesia as {attributes: {Provinsi, Kasus_Posi, Kasus_Meni, Kasus_Semb}}, i}
          <tr>
            <th class="border border-black px-4 py-2">{i+1}</th>
            <th class="border border-black px-4 py-2">{Provinsi}</th>
            <th class="border border-black px-4 py-2">{Kasus_Posi}</th>
            <th class="border border-black px-4 py-2">{Kasus_Meni}</th>
            <th class="border border-black px-4 py-2">{Kasus_Semb}</th>
          </tr>
          {:else}
            <tr>
            <th class="border border-black px-4 py-2">{@html spinner}</th>
            <th class="border border-black px-4 py-2">{@html spinner}</th>
            <th class="border border-black px-4 py-2">{@html spinner}</th>
            <th class="border border-black px-4 py-2">{@html spinner}</th>
            <th class="border border-black px-4 py-2">{@html spinner}</th>
          </tr>
        {/each}
        </tbody>
      </table>
    </div>
    </div>
    
    <div class="p-3">
    <h1 class="text-center text-2xl"> Country </h1>
    <div class="md:block overflow-auto h-64 my-3" style="height:30vh;">
      <table class="table-auto">
        <thead>
          <tr>
            <th class="border border-black px-4 py-2">No</th>
            <th class="border border-black px-4 py-2">Country</th>
            <th class="border border-black px-4 py-2">Positive</th>
            <th class="border border-black px-4 py-2">Deaths</th>
            <th class="border border-black px-4 py-2">Recovered</th>
          </tr>
        </thead>
      <tbody>
      {#each country as {attributes: {Country_Region, Confirmed, Deaths, Recovered}}, i}
        <tr>
          <th class="border border-black px-4 py-2">{i+1}</th>
          <th class="border border-black px-4 py-2">{Country_Region}</th>
          <th class="border border-black px-4 py-2">{Confirmed}</th>
          <th class="border border-black px-4 py-2">{Deaths}</th>
          <th class="border border-black px-4 py-2">{Recovered}</th>
        </tr>
        {:else}
        <tr>
          <th class="border border-black px-4 py-2">{@html spinner}</th>
          <th class="border border-black px-4 py-2">{@html spinner}</th>
          <th class="border border-black px-4 py-2">{@html spinner}</th>
          <th class="border border-black px-4 py-2">{@html spinner}</th>
          <th class="border border-black px-4 py-2">{@html spinner}</th>
        </tr>
      {/each}
      </tbody>
    </table>
    </div>
    </div>
  </div>
</main>
<div class="flex justify-center items-center m-auto p-6">
  <h1> Thanks for <a href="http://kawalcorona.com/" class="no-underline text-center"> Kawalcorona.com </a>
  <p class="text-center"> copyright 2020 by sidik jari </p>
</div>

<style global>
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  body {
    padding: 0;
    background-color: #ddd;
  }
</style>
