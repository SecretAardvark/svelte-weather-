<script lang="ts">
  import { onMount } from "svelte";
  import "@picocss/pico";
  import AccuWeatherClient from "accu-weather-api-wrapper";

  let currentWeather;
  let currentTemp: number;
  let location = "Portland, OR";
  let description: string;
  let icon;
  let getWeather = async () => {
    const weather = new AccuWeatherClient({
      apikey: "sbewALxc4hIHOgvHhG9kDWrsOKfpLoO7",
    });
    //await weather.location.citySearch("Portland, or").then(console.log);
    // await weather.forecast.getDailyForecast(1, "350473").then(console.log);
    currentWeather = await weather.currentConditions.currentCondition("350473");

    console.log(currentWeather);

    currentTemp = currentWeather[0].Temperature.Imperial.Value;
    description = currentWeather[0].WeatherText;
    icon = `https://www.accuweather.com/images/weathericons/${currentWeather[0].WeatherIcon}.svg`;
  };

  onMount(() => getWeather());

  //TODO: detect location via ip address to get current weather?
  //TODO: Fix the icon.
  //TODO: Components: 'Current Weather' card (mvp on this page), '5 day forecast' card (5 smaller daily cards?)
</script>

<main class="container-fluid">
  <article>
    <header><h3>Weather in {location}</h3></header>
    <div class="container">
      <div class="outer">
        <img src={icon} style="padding-right:10px;" />
        <div class="inner">
          <h2>{currentTemp}°f</h2>
          <h3>{description}</h3>
        </div>
      </div>
    </div>
  </article>
</main>

<style>
  .outer {
    display: flex;
    justify-content: center;
    align-items: center;
    /* border: 1px solid black; */
    text-align: right;
  }
  .inner {
    display: grid;
    text-align: center;
  }
  header {
    text-align: center;
  }
</style>
