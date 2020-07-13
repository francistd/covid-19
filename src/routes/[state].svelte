<script context="module">
  import stateNames from "../data/stateNames.js";
  import request from "../data/request.js";

  export async function preload(page) {
    const state = page.params["state"];
    if (stateNames.find(s => s.abbreviation === state) === undefined) {
      this.error(404, "State Not Found");
      return;
    }

    const fullStateName = stateNames.find(s => s.abbreviation === state).name;

    try { 
      const stats = await request.stateStats(state);
      const historic = await request.historicState(state);
      return { state:fullStateName, stats, historic };
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
  export let historic;
</script>

<svelte:head>
  <title>Covid-19 - {state}</title>
</svelte:head>

<div class="section header">
  <h1>Covid- {state}</h1>
</div>

<CovidStat {...stats}/>
<CovidChart historicData={historic} title="Covid 19 - {state}"/>
