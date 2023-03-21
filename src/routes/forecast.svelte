<script>
  import ForecastDay from "./forecastDay.svelte";

  export let forecastData;
</script>

<div class="container-fluid">
  <div class="grid">
    <ForecastDay dailyForecast={forecastData.DailyForecasts[0]} />
    <article>day1</article>
    <article>day2</article>
    <article>day3</article>
    <article>day4</article>
  </div>
</div>
