<script>
  export let location;
  export let icon;
  export let currentTemp;
  export let description;
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
