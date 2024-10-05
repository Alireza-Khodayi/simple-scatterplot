<script>
    import { fly } from "svelte/transition"

    export let data;
    export let xScale;
    export let yScale;
    export let width;

    let toolTipWidth;

    $: x = xScale(data.grade);
    $: y = yScale(data.hours);

    const xNudge = 15;
    const yNudge = 30;

    $: isFallingOffChart = toolTipWidth + x > width
    $: xPosition = isFallingOffChart ? x - toolTipWidth - xNudge : x + xNudge
    $: yPosition = y + yNudge;

</script>
<div
    in:fly={{ y: -20 }}
    out:fly={{ y: 20 }}
    bind:clientWidth={toolTipWidth}
    class="tooltip" style="left: {xPosition}px; top: {yPosition}px">
        <h3 class="title">{data.name}<span>{data.grade}%</span></h3>
        <p class="text">{data.hours} hours studied</p>
</div>


<style>
    .tooltip {
        position: absolute;
        background: white;
        padding: 8px 6px;
        box-shadow: rgba(0, 0, 0, 0.15) 2px 3px 8px;
        border-radius: 3px;
        pointer-events: none;
        transition: top 300ms ease, left 300ms ease;

    }
    .title {
        font-size: 1rem;
        font-weight: 500;
        margin-bottom: 6px;
        width: 100%;
    }
    .title span {
        font-size: 80%;
        padding: 3px 3px;
        background: #dda0ddd0;
        margin-left: 2px;
        border-radius: 3px;
        display: inline-block;
        vertical-align: middle;
        color: rgba(0, 0, 0, 0.7);
    }
    .text {
        font-size: 0.8rem;
        font-weight: 300;
        text-transform: uppercase;
        color:#0f0f0f
    }
</style>