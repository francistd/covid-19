<script>
import CovidStat from '../components/CovidStat.svelte';
import CovidChart from '../components/CovidChart.svelte';
import TableContainer from '../components/TableContainer.svelte';
</script>

<svelte:head>
  <title>Covid-19 Tracker</title>
</svelte:head>

<div class="section header">
<h1>Covid-19 -US</h1>
</div>

<CovidStat/>
<CovidChart/>
<TableContainer/>

