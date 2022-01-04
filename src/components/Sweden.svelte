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
    const url = `https://api.covid19api.com/country/sweden/status/confirmed?from=${yesterday}&to=${today}`;
    const res = await fetch(url);
    const data = await res.json();

    dataPoint = data;

    for (var i = 0; i < 1; i++) {
      console.log(dataPoint[i]);
      country = dataPoint[i].Country;
      confirmedCases = dataPoint[i].Cases;
      latestUpdate = dataPoint[i].Date;
    }
  };

  let dataPoint = [];
  let country = "";
  let confirmedCases: number;
  let latestUpdate: string;
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
    <h1 class="text-4xl pt-2">Country: <b>{country}</b></h1>
    <p class="text-xl mt-5">Confirmed Cases: <b>{confirmedCases}</b></p>
    <p class="text-xl pt-2">
      Latest update: <b>{moment(latestUpdate).format("MMMM Do YYYY, h:mm a")}</b
      >
    </p>
    <!-- {#each dataPoint as data} -->
    <!-- <p class="text-xl">Confirmed Cases: <b>{data.Cases}</b></p> -->

    <!-- <p class="text-xl pt-2">
          Latest update: <b>{moment(data.Date).format("MMMM Do YYYY, h:mm a")}</b>
        </p>
      {/each} -->
  </div>
</div>
