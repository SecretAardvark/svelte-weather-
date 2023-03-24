<script lang="ts">
  import { onMount } from "svelte";
  import CurrentWeather from "./currentWeather.svelte";
  import "@picocss/pico";
  import AccuWeatherClient, {
    type IDailyForecastData,
  } from "accu-weather-api-wrapper";
  import Forecast from "./forecast.svelte";
  import ForecastDay from "./forecastDay.svelte";

  let currentWeather;
  let forecastData: IDailyForecastData;
  let currentTemp: number;
  let location = "Portland, OR";
  let description: string;
  let icon: string;
  let getWeather = async () => {
    const weather = new AccuWeatherClient({
      apikey: "sbewALxc4hIHOgvHhG9kDWrsOKfpLoO7",
    });

    currentWeather = await weather.currentConditions.currentCondition("350473");
    forecastData = await weather.forecast.getDailyForecast(5, "350473");

    //     console.log(forecastData);

    currentTemp = currentWeather[0].Temperature.Imperial.Value;
    description = currentWeather[0].WeatherText;
    icon = `https://www.accuweather.com/images/weathericons/${currentWeather[0].WeatherIcon}.svg`;
  };

  onMount(() => getWeather());

  //MVP is basically finished here. It still needs some styling and a few more features:
  //TODO: detect location via ip address to get current weather?
  //TODO: Display more data when clicking on show more
</script>

{#if currentWeather}
  <CurrentWeather {location} {icon} {currentTemp} {description} />
{:else}
  <article aria-busy="true" />
{/if}

{#if forecastData}
  <Forecast {forecastData} />
{:else}
  <article aria-busy="true" />
{/if}
