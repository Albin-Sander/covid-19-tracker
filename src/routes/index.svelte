<script lang="ts">
  import { onMount } from "svelte";
  import moment from "moment";

  onMount(() => {
    fetchData();
  });
  const fetchData = async () => {
    const url =
      "https://api.covid19api.com/country/sweden/status/confirmed?from=2021-12-29T00:00:00Z&to=2021-12-30T00:00:00Z";
    const res = await fetch(url);
    const data = await res.json();

    console.log(data[0]);
    dataPoint = data;
  };

  let dataPoint = [];
  let country: string;
</script>

<div class="border-solid border-2 p-20 mt-20 shadow-lg">
  <h1 class="text-4xl">Covid 19 Tracker</h1>

  <!-- <button on:click={() => console.log(dataPoint)}>test</button> -->
  <div class="mt-5">
    {#each dataPoint as data}
      <p class="text-xl">Cases: <b>{data.Cases}</b></p>
      <p class="text-xl pt-2">Country: <b>{data.Country}</b></p>
      <p class="text-xl pt-2">
        Latest update: <b
          >{moment(data.Date).format("MMMM Do YYYY, h:mm:ss a")}</b
        >
      </p>
    {/each}
  </div>
</div>
