<script lang="ts">
  import { onMount } from "svelte";
  import moment from "moment";

  onMount(() => {
    fetchData();
  });
  const fetchData = async () => {
    const today = moment().startOf("day").format("YYYY-MM-DD");
    const yesterday = moment()
      .subtract(1, "day")
      .startOf("day")
      .format("YYYY-MM-DD");
    const url = `https://api.covid19api.com/country/norway/status/confirmed?from=${yesterday}&to=${today}`;
    const res = await fetch(url);
    const data = await res.json();

    dataPoint = data;
  };

  let dataPoint = [];
</script>

<div
  class="border-solid border-2 border-indigo-600 p-20 mt-20 shadow-lg dark:bg-gray-700 rounded-md flex flex-col"
>
  <div class="flex flex-row justify-between">
    <img
      src="./static/refresh.svg"
      class="w-8 h-8  hover:cursor-pointer hover:bg-gray-600 rounded-md"
      alt="refresh icon"
      on:click={fetchData}
    />
  </div>
  <div class="mt-5">
    {#each dataPoint as data}
      <h1 class="text-4xl pt-2">Country: <b>{data.Country}</b></h1>
      <p class="text-xl">Cases: <b>{data.Cases}</b></p>

      <p class="text-xl pt-2">
        Latest update: <b>{moment(data.Date).format("MMMM Do YYYY, h:mm a")}</b>
      </p>
    {/each}
  </div>
</div>
