<script lang="ts">
  import Norway from "../components/Norway.svelte";
  import Sweden from "../components/Sweden.svelte";
  import SearchCard from "../components/SearchCard.svelte";
  import Denmark from "../components/Denmark.svelte";
  import Finland from "../components/Finland.svelte";
</script>

<div>
  <div class="flex justify-around">
    <Sweden />
    <Norway />
  </div>
  <div class="flex justify-center">
    <SearchCard />
  </div>
  <div class="flex justify-around">
    <Denmark />
    <Finland />
  </div>
</div>
