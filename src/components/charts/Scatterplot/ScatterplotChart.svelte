<script>
  import { scaleLinear } from 'd3-scale'
  import AxisX from './AxisX.svelte';
	import AxisY from './AxisY.svelte';
	import ScatterplotTooltip from './ScatterplotTooltip.svelte';
    
  export let data

  const margin = {
    top: 20,
    right: 20,
    bottom: 20,
    left: 0,
  }

  export let width = 400;
  $: innerWidth = width - margin.left - margin.right
  $: xScale = scaleLinear().domain([0,100]).range([0,innerWidth])
    
  export let height = 400;
  let innerHeight = height - margin.top - margin.bottom
  let yScale = scaleLinear().domain([0,60]).range([innerHeight,0])
    
  let hoveredData;
  
</script>
  
<div class="chart-container" bind:clientWidth={width}>
  <svg {width} {height}>
    <g transform={`translate(${margin.left}, ${margin.top})`}>
      <AxisX {xScale} width={innerWidth} height={innerHeight}/>
      <AxisY {yScale} width={innerWidth}/>
      {#each data as d }
        <circle 
          cx={xScale(d.grade)}
          cy={yScale(d.hours)}
          r={10}
          fill='purple'
          stroke='black'
          stroke-width='1'
          on:mouseover={() => {
            hoveredData = d
          }}
          on:focus={() => {
            hoveredData = d
          }}
        />
      {/each}
    </g>
  </svg>
  {#if hoveredData}
      <ScatterplotTooltip data={hoveredData} {xScale} {yScale} width={innerWidth}/>
  {/if}
</div>

  <style>
    :global(.tick text, .axis-title) {
      font-weight: 400; 
      font-size: 12px;
      fill: #8f8f8f;
    }
  </style>