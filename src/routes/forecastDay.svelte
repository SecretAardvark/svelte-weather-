<script lang="ts">
  export let dailyForecast;
  import moment from "moment";

  let extraDetail = false;
  const date = moment(dailyForecast.Date).format("M/DD");
  let icon = `https://www.accuweather.com/images/weathericons/${dailyForecast.Day.Icon}.svg`;
  let hiTemp = `Hi: ${dailyForecast.Temperature.Maximum.Value}${dailyForecast.Temperature.Maximum.Unit}`;
  let loTemp = `Lo: ${dailyForecast.Temperature.Minimum.Value}${dailyForecast.Temperature.Minimum.Unit}`;
</script>

<article>
  <header><h4>{date} {dailyForecast.Day.IconPhrase}</h4></header>

  <img src={icon} alt={dailyForecast.Day.IconPhrase} />
  <h5>
    {hiTemp}
    {loTemp}
  </h5>

  {#if extraDetail}
    <!-- <p>{dailyForecast.}</p> -->
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
  button {
    width: 50%;
  }
  img {
    height: 100px;
    width: 100px;
  }
  footer {
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
