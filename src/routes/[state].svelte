<script context="module">
  import stateNames from "../data/stateNames.js";
  import request from "../data/request.js";

  export async function preload(page) {
    const state = page.params["state"];
    if (stateNames.find(s => s.abbreviation === state) === undefined) {
      this.error(404, "State Not Found");
      return;
    }

    try { 
      const stats = await request.stateStats(state);
      return { state, stats };
    } catch (e) {
      this.error(500, "There was an error calling the api try again later.");
      return;
    }
  }
</script>

<script>
  import CovidStat from "../components/CovidStat.svelte";
  import CovidChart from "../components/CovidChart.svelte";
  import TableContainer from "../components/TableContainer.svelte";
  export let state;
  export let stats;
</script>

<svelte:head>
  <title>Covid-19 - {state}</title>
</svelte:head>

<div class="section header">
  <h1>Covid- {state}</h1>
</div>

<CovidStat {...stats}/>
<CovidChart />
