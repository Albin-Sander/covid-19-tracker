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

<div>
  <h1>Covid 19 Tracker</h1>

  <button on:click={() => console.log(dataPoint)}>test</button>
  {#each dataPoint as data}
    Cases: {data.Cases}
    {data.Country}
    {moment(data.Date).format("MMMM Do YYYY, h:mm:ss a")}
  {/each}
</div>
