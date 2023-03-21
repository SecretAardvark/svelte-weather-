<script>
  export let dailyForecast;
  let extraDetail = false;
</script>

<article>
  {dailyForecast.Date}
  {dailyForecast.Day.IconPhrase}
  <footer>
    <!-- <a
      role="button"
      on:click={() => {
        extraDetail = !extraDetail;
      }}
    >
      see more
    </a> -->
  </footer>
</article>
