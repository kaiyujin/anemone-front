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
const TAU = 2 * Math.PI
function createTt (target, w, h, ir, or) {
  const svg = d3.select('#d3figure').append('svg').attr('width', w).attr('height', h)
  const g = svg.append('g')
    .attr('transform', 'translate(' + w / 2 + ',' + h / 2 + ')')
  const arc = d3.arc().innerRadius(ir).outerRadius(or)
    .padAngle(0.01).cornerRadius(3)
  g.append('path').datum({startAngle: 0, endAngle: TAU}).style('fill', '#ddd').attr('d', arc)
  return g
}
const T = 0.08333333333333333333
function t2a (h, m) {
  return h * T + (m && m > 0 && m < 60 ? (m / 60 * T) : 0)
}
export default {
  mounted () {
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
    g.append('path').datum({startAngle: TAU * 0.3, endAngle: TAU * 0.5})
      .style('fill', '#e34f26')
      .style('cursor', 'pointer')
      .attr('d', arc)
      .on('click', function (d, idx) {
        const g2 = createTt('d3figure', 200, 200, 80, 100)
        g2.append('path').datum({startAngle: TAU * t2a(3), endAngle: TAU * t2a(5, 30)}).style('fill', '#e34f26').attr('d', arc)
        g2.append('path').datum({startAngle: TAU * t2a(6), endAngle: TAU * t2a(11, 59)}).style('fill', '#e34f26').attr('d', arc)
      })
    g.append('path').datum({startAngle: TAU * t2a(6), endAngle: TAU * t2a(7)}).style('fill', '#e34f26').attr('d', arc)
    g.append('path').datum({startAngle: TAU * t2a(7), endAngle: TAU * t2a(8)}).style('fill', '#e34f26').attr('d', arc)
    g.append('path').datum({startAngle: TAU * t2a(8), endAngle: TAU * t2a(9, 30)}).style('fill', '#e34f26').attr('d', arc)
    g.append('rect').attr('x', -40).attr('y', -40).attr('width', 80).attr('height', 80).attr('fill', '#cd5c5c')
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
