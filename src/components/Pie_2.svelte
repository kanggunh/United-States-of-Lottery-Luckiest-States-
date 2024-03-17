<script>
    import { onMount } from 'svelte';
    import * as d3 from 'd3';
    import { tweened } from 'svelte/motion';
    import { afterUpdate } from 'svelte';
    import { cubicOut } from 'svelte/easing';
  
    export let index2; // Placeholder for interactive functionality
    export let width2; // Adjusted to match the image aspect ratio
    export let height2;
  
    let data = [
      { label: 'Prizes & Jackpots', value: 50, color: '#FF6384' , description: 'Only <b>50%</b> of all ticket sales go to funding the Powerball prizes and jackpots'},
      { label: 'Charities', value: 35, color: '#36A2EB', description: '<b>35%</b> of all ticket sales go to causes and charities supported by lotteries across the country'},
      { label: 'Powerball lottery organisation', value: 9, color: '#FFCE56', description: '<b>6%</b> of ticket sales go to retailer commissions.'},
      { label: 'Retailers', value: 6, color: '#4BC0C0', description: '<b>9%</b> of ticket sales go to operating expenses of the Powerball lottery organisation.'},
    ];
  
    const tweenedValue = tweened(0, {
        duration: 1000,
        easing: cubicOut
    });
  
    function createPieChart(datum, svgElement) {
        const svg = d3.select(svgElement);
        svg.selectAll("*").remove();
    
        const radius = Math.min(width2, height2) / 3.1;
        const arc = d3.arc().innerRadius(50).outerRadius(radius);
        const labelArc = d3.arc().outerRadius(radius - 50).innerRadius(radius - 50);
        const pieData = d3.pie().value(d => d.value)([
            { value: datum.value },
            { value: 100 - datum.value },
        ]);
    
        svg
            .attr('viewBox', [-width2/2, -height2/2, width2, height2])
            .append('g')
            .attr('stroke', 'black')
            .selectAll('path')
            .data(pieData)
            .join('path')
            .attr('fill', (d, i) => (i === 0 ? datum.color : '#e1e1e1'))
            .attr('d', arc)
            .transition()
            .duration(750)
            .attrTween('d', d => {
                const i = d3.interpolate(d.startAngle + 0.1, d.endAngle);
                return t => {
                d.endAngle = i(t);
                return arc(d);
                };
            });
        svg.append('text')
            .attr('text-anchor', 'middle')
            .attr('alignment-baseline', 'middle')
            .attr('fill', 'black')
            .attr('font-size', '3em')
            .text(`${datum.value}%`);
    }

    onMount(() => {
      const currentData = data[index2];
      const svgElement = `#chart2-${index2}`;
      createPieChart(currentData, svgElement);
  
      tweenedValue.set(currentData.value);
    });

    afterUpdate(() => {
        if (width2 && height2) {
        const currentData = data[index2];
        const svgElement = `#chart2-${index2}`;
        createPieChart(currentData, svgElement);
        }
    });
  </script>
  
  <svg id="chart2-{index2}" width="{width2}" height="{height2}"></svg>
  
  <style>
    svg {
      display: inline-block;
      margin: 0 auto;
    }
  </style>

  