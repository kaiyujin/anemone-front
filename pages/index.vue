<template>
  <section class="container">
    <div>
      <logo/>
      <h1 class="title">
        anemone
      </h1>
      <div class="links">
        <figure class="chart" data-percent="75">
          <svg width="200" height="200">
            <circle class="outer" cx="95" cy="95" r="85" transform="rotate(-90, 95, 95)"/>
          </svg>
	</figure>
      </div>
    </div>
  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

svg .outer {
  stroke: #e34f26;
}

.outer {
  fill: transparent;
  stroke: #333;
  stroke-width: 20;
  stroke-dasharray: 534;
  transition: stroke-dashoffset 1s;
  -webkit-animation-play-state: running;
  
  /* firefox bug fix - won't rotate at 90deg angles */
  -moz-transform: rotate(-89deg) translateX(-190px);
}
.chart:hover .outer {
  stroke-dashoffset: 534 !important;
  -webkit-animation-play-state: paused;
}
</style>
