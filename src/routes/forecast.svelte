<script>
  import { each } from "svelte/internal";
  import ForecastDay from "./forecastDay.svelte";

  export let forecastData;
</script>

<div class="container">
  <div class="container">
    <header><h4>{forecastData.Headline.Text}</h4></header>
  </div>
  <div class="grid container">
    {#each forecastData.DailyForecasts as foreCast}
      <ForecastDay dailyForecast={foreCast} />
    {/each}
  </div>
</div>
