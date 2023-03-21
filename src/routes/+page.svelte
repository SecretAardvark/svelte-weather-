<script lang="ts">
  import { onMount } from "svelte";
  import CurrentWeather from "./currentWeather.svelte";
  import "@picocss/pico";
  import AccuWeatherClient, {
    type IDailyForecastData,
  } from "accu-weather-api-wrapper";
  import Forecast from "./forecast.svelte";

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
    //await weather.location.citySearch("Portland, or").then(console.log);
    // await weather.forecast.getDailyForecast(1, "350473").then(console.log);
    currentWeather = await weather.currentConditions.currentCondition("350473");
    forecastData = await weather.forecast.getDailyForecast(5, "350473");

    console.log(currentWeather);
    console.log(forecastData);

    currentTemp = currentWeather[0].Temperature.Imperial.Value;
    description = currentWeather[0].WeatherText;
    icon = `https://www.accuweather.com/images/weathericons/${currentWeather[0].WeatherIcon}.svg`;
  };

  onMount(() => getWeather());

  //TODO: detect location via ip address to get current weather?
  //TODO: Fix the icon.
  //TODO: Components: 'Current Weather' card (mvp on this page), '5 day forecast' card (5 smaller daily cards?)
</script>

<CurrentWeather {location} {icon} {currentTemp} {description} />
<!-- <h2>{forecastData["Headline"].Text}</h2> -->
<Forecast {forecastData} />
