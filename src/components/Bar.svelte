<script>
    import * as d3 from 'd3';
    import { onMount } from 'svelte';
    import BarTooltip from "./barTooltip.svelte";

    let stateData = [];

    onMount(async () => {
        const res = await fetch(
            'winning_state_count.csv',
        );
        const csv = await res.text();
        await d3.csvParse(csv, data => {
        stateData.push(data);
        });
        stateData = stateData;
    });

    console.log(stateData);

    let width = 800;
    let height = 1000;
    let hovered=null;

    const margin = { top: 20, right: 50, bottom: 20, left: 120 };
    const innerHeight = height - margin.top - margin.bottom;
    const innerWidth = width - margin.left - margin.right;

    $: xDomain = stateData.map((d) => d.state);
    $: yDomain = stateData.map((d) => +d.count);

    $: yScale = d3.scaleBand().domain(xDomain).range([0, innerHeight]).padding(0.05);
    $: xScale = d3.scaleLinear()
        .domain([0, Math.max.apply(null, yDomain)])
        .range([0, innerWidth]);
</script>

<div class='chart-container' on:mouseout={()=>{hovered=null}}>
  <svg {width} {height}>

    <g transform={`translate(${margin.left},${margin.top})`}>
      {#each xScale.ticks() as tickValue}
        <g transform={`translate(${xScale(tickValue)},0)`}>
          <line y2={innerHeight} stroke="gray" />
          <text text-anchor="middle" dy=".7em" y={innerHeight + 3}>
            {tickValue}
          </text>
        </g>
      {/each}
      {#each stateData as d}
        <text
          text-anchor="end"
          x="-3"
          dy=".3em"
          y={yScale(d.state) + yScale.bandwidth() / 2}
        >
          {d.state}
        </text>
        <rect
          x="0"
          y={yScale(d.state)}
          width={xScale(d.count)}
          height={hovered ? hovered == d ?yScale.bandwidth()+1.5:yScale.bandwidth():yScale.bandwidth()}
          opacity={hovered ? hovered == d ? "1" : ".3" : "1"}
          fill= #86A8E7;
          on:mouseover={() => {hovered=d}}
        />
      {/each}
    </g>
  </svg>

  {#if hovered}
    <BarTooltip data = {hovered} {xScale} {yScale}/>
  {/if}


</div>




<style>

  @import url('https://fonts.googleapis.com/css2?family=Protest+Strike&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Roboto+Serif:ital,opsz,wght@0,8..144,100..900;1,8..144,100..900&display=swap');

  text {
    font-size: 11px;
  }

  rect {
    fill: #86A8E7;

  }

  line {
    opacity: 0.3;
  }



</style>