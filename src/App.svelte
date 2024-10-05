<script>
  import data from "$data/data";
  import { scaleLinear } from 'd3-scale'

  let width = 400;
  let xScale = scaleLinear().domain([0,100]).range([0,width])
  
  let height = 400;
  let yScale = scaleLinear().domain([0,100]).range([height,0])
    
</script>

<svg {width} {height}>
{#each data as d }
  <circle 
    cx={xScale(d.grade)}
    cy={yScale(d.hours)}
    r={10}
    fill='purple'
    stroke='black'
    stroke-width='1'
  />
{/each}
</svg>

<!-- <p>{d.name} studied for {d.hours} hours and scored {d.grade}%</p>  -->
