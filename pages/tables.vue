<template>
  <section class="container">
    <div>
	<figure id="d3figure">
	</figure>
    </div>
  </section>
</template>

<script>
import * as d3 from 'd3'
export default {
  mounted () {
    console.log(d3)
    const TAU = 2 * Math.PI
    const width = 200
    const height = 200
    const start = 0.1
    const end = 0.3
    const svg = d3.select('#d3figure').append('svg').attr('width', width).attr('height', height)
    const g = svg.append('g')
      .attr('transform', 'translate(' + width / 2 + ',' + height / 2 + ')')
    const arc = d3.arc().innerRadius(80).outerRadius(100)
      .padAngle(0.01).cornerRadius(3)
    g.append('path').datum({startAngle: 0, endAngle: TAU}).style('fill', '#ddd').attr('d', arc)
    g.append('path').datum({startAngle: TAU * start, endAngle: TAU * end}).style('fill', '#e34f26').attr('d', arc)
    g.append('path').datum({startAngle: TAU * 0.3, endAngle: TAU * 0.4})
      .style('fill', '#e34f26')
      .style('cursor', 'pointer')
      .attr('d', arc)
      .on('click', function (d, idx) {
        alert(idx)
      })
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
}

svg .inner{
  fill: transparent;
  stroke: #333;
  stroke-width: 15;
  stroke-dasharray: 534;
  transition: stroke-dashoffset 1s;
  -webkit-animation-play-state: running;
  
  /* firefox bug fix - won't rotate at 90deg angles */
  -moz-transform: rotate(-89deg) translateX(-190px);
}

svg .outer {
  stroke: #e34f26;
}

svg .outer2 {
  stroke: #999;
}
svg .outer3 {
  stroke: #e34f26;
}
</style>
