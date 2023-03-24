<script lang="ts">
  import moment from "moment";

  export let dailyForecast;
  export let unit;

  let extraDetail = false;
  const date = moment(dailyForecast.Date).format("M/DD");
  let icon: string = `https://www.accuweather.com/images/weathericons/${dailyForecast.Day.Icon}.svg`;
  let hiTemp: string = `Hi: ${dailyForecast.Temperature.Maximum.Value}${dailyForecast.Temperature.Maximum.Unit}`;
  let loTemp: string = `Lo: ${dailyForecast.Temperature.Minimum.Value}${dailyForecast.Temperature.Minimum.Unit}`;
</script>

<article>
  <header><h4>{date} {dailyForecast.Day.IconPhrase}</h4></header>

  <img src={icon} alt={dailyForecast.Day.IconPhrase} />

  {#if extraDetail}
    <h5>
      {hiTemp}
      {loTemp}
    </h5>
  {/if}
  <footer>
    <button
      on:click={() => {
        extraDetail = !extraDetail;
      }}
    >
      {#if !extraDetail}
        see more
      {:else}
        close
      {/if}
    </button>
  </footer>
</article>

<style>
  article {
  }
  button {
    width: 50%;
    min-width: 100px;
  }
  img,
  h5 {
    display: block;
    height: 100px;
    width: 100px;
    margin: 0 auto;
  }
  footer,
  header {
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
