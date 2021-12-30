<script lang="ts">
  import { onMount } from "svelte";
  import moment from "moment";
  import Layout from "./__layout.svelte";

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

<div
  class="border-solid border-2 border-indigo-600 p-20 mt-20 shadow-lg dark:bg-gray-700 rounded-md flex flex-col"
>
  <div class="flex flex-row justify-between">
    <h1 class="text-4xl  border-solid border-b-2 border-indigo-600">
      Covid 19 Tracker
    </h1>

    <img
      src="./static/refresh.svg"
      class="w-8 h-8  hover:cursor-pointer hover:bg-gray-600 rounded-md"
      alt="refresh icon"
      on:click={fetchData}
    />
  </div>
  <!-- <button on:click={() => console.log(dataPoint)}>test</button> -->
  <div class="mt-5">
    {#each dataPoint as data}
      <p class="text-xl">Cases: <b>{data.Cases}</b></p>
      <p class="text-xl pt-2">Country: <b>{data.Country}</b></p>
      <p class="text-xl pt-2">
        Latest update: <b>{moment(data.Date).format("MMMM Do YYYY, h:mm a")}</b>
      </p>
    {/each}
  </div>
</div>
