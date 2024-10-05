<script>
	import { tick } from "svelte";

    export let yScale;
    export let width;

    let yTicks = yScale.ticks(3);
</script>

<g class="axis y">
    {#each yTicks as tick, i}
    <g class="tick" transform={`translate(0, ${yScale(tick)})`}>
        <line 
            x1="0" 
            y1="0" 
            y2="2" 
            x2={width} 
            stroke={i === 0 ? '#8f8f8f' : '#e5e7eb'}
        />
        <text x="0" y="-5">{tick} {i === yTicks.length - 1 ? ' Hours studied' : ''}</text>
    </g>
    {/each}
</g>
