<script context="module">
  import requests from "../data/request.js";

  export async function preload() {
    try {
      const usStats = await requests.usStats();
      const historic = await requests.historicUS();
      const statesData = await requests.statesData();
      return { usStats, historic, statesData };
    } catch (e) {
      this.error(500, 'There was an error calling the api try again later.');
      return;
    }
  }
</script>

<script>
  import CovidStat from "../components/CovidStat.svelte";
  import CovidChart from "../components/CovidChart.svelte";
  import TableContainer from "../components/TableContainer.svelte";

  export let usStats;
  export let historic;
  export let statesData;
</script>

<svelte:head>
  <title>Covid-19 Tracker</title>
</svelte:head>

<div class="section header">
  <h1>Covid-19 -US</h1>
</div>

<CovidStat {...usStats} />
<CovidChart historicData= {historic} title="US Covid-19"/>
<TableContainer data={statesData} />
