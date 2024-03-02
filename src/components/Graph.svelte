<script>
    import * as d3 from 'd3';
    import { onMount } from 'svelte'; 
    import Tooltip from '../components/Tooltip.svelte';

    let width= 460;
    let height= 400;
    const margin = { top: 20, right: 20, bottom: 50, left: 90 };
    const innerHeight = height - margin.top - margin.bottom;
    const innerWidth = width - margin.left - margin.right;

    let data_lottery = []
    let xTicks = []
    let yTicks = []

    onMount(async () => {
        const res = await fetch(
            'lottery_stats.csv',
        );
        const csv = await res.text();
        await d3.csvParse(csv, data => {
        data_lottery.push(data);
        });
        data_lottery = data_lottery;
    });

    let xAxis;
	let yAxis;

    console.log(data_lottery);

    import { max } from "d3-array";
    import { min} from "d3-array";

    $: xScale = d3.scaleLinear()
        .domain([min(data_lottery, d => d.income_two), max(data_lottery, d => d.income_two)])
        .range([margin.left, width - margin.right]);


    $: yScale = d3.scaleLinear()
        .domain([min(data_lottery, d => d.sales_in_million), max(data_lottery, d => d.sales_in_million)])
        .range([height - margin.bottom, margin.top]);

    $: {
        d3.select(yAxis)
            .call(d3.axisLeft(yScale));
        
        d3.select(xAxis)
				.call(d3.axisBottom(xScale))
				.selectAll('.tick > text')
				.attr('y', 0)
				.attr('dy', '0.35em')
				.attr('dx', '-1em')
				.attr('text-anchor', 'end')
				.attr('transform', 'rotate(-90)');
	}

    let hoveredData;
    $: console.log(hoveredData);
    $: console.log(window.innerHeight);
    $: console.log(window.innerWidth);

</script>

{#if hoveredData}
    <Tooltip data={hoveredData} {xScale} {yScale} />
{/if}

<!-- svelte-ignore a11y-no-static-element-interactions -->
<svg {width} {height} 
    on:mouseleave={() => {
        setTimeout(() => {
            hoveredData = null;
        }, 100);
    }}
>
   
    {#each data_lottery as point}
        <!-- svelte-ignore a11y-mouse-events-have-key-events -->
        <circle 
        cx={xScale(point.income_two)} 
        cy={yScale(point.sales_in_million)} 
        r={hoveredData && hoveredData == point ? "12.5": "8"}
        opacity={hoveredData ? hoveredData == point ? "0.8": "0.45" : "0.8"}
        on:mouseover={() => {hoveredData = point;}}
         />
    {/each}

    <g transform="translate(0, {height - margin.bottom})"
    bind:this={xAxis} />

    <g transform="translate({margin.left}, 0)"
    bind:this={yAxis} />
</svg>


<style>
    circle {
        stroke: gray;
        fill: lightblue;
        transition: all 300ms ease;
    }

    svg {
        align-items: center;
        margin-right: 60px;
    }
</style>