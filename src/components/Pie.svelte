<script>
    import { onMount } from 'svelte';
    import { tweened } from 'svelte/motion';
    import * as d3 from 'd3';
    import { afterUpdate } from 'svelte';
    import { cubicOut } from 'svelte/easing';
  
    export let index;
    export let width;
    export let height;
  
    // Dummy data, replace with your actual data
    let datasets = [
        { label: 'Share with Family', value: 83, color: '#00a1e4', description: '83% of lottery winners share their jackpot with at least 1 family member.' },
        { label: 'Donate to Charity', value: 40, color: '#ff6384', description: '40% of lottery jackpot winners choose to donate to charity.' },
        { label: 'Buy a Home', value: 66, color: '#ffcd56', description: '66% of lottery winners buy a new home.' },
        { label: 'Vacation Outside U.S.', value: 20, color: '#4bc0c0', description: '20% of lottery winners decide to take a vacation outside the U.S.' }
    ];

    // Tweened value for the pie chart animation
    const tweenedValue = tweened(0, {
        duration: 1000,
        easing: cubicOut
    });
  
    // This function creates a pie chart in the given svg element
    function createPieChart(datum, svgElement) {
        const svg = d3.select(svgElement);
        svg.selectAll("*").remove(); // Clear the SVG to redraw
    
        const radius = Math.min(width, height) / 5;
        const arc = d3.arc().innerRadius(0).outerRadius(radius);
        const labelArc = d3.arc().outerRadius(radius - 50).innerRadius(radius - 50);
        const pieData = d3.pie().value(d => d.value)([
            { value: datum.value },
            { value: 100 - datum.value },
        ]);
    
        svg
            .attr('viewBox', [-width/1.5, -height/2.3, width, height])
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
            .attr('transform', d => `translate(${labelArc.centroid(pieData[0])})`)
            .attr('text-anchor', 'middle')
            .attr('alignment-baseline', 'middle')
            .attr('fill', 'white')
            .attr('font-size', '3em')
            .text(`${datum.value}%`);
        svg.append('text')
            .attr('transform', d => `translate(-450,-150)`)
            .attr('text-anchor', 'right')
            .attr('alignment-baseline', 'right')
            .attr('fill', 'black')
            .attr('font-size', '1.5em')
            .text(`${datum.description}%`);
    }
  
    let currentData = datasets[0];

    onMount(() => {
      const currentData = datasets[index];
      const svgElement = `#chart-${index}`;
      createPieChart(currentData, svgElement);
  
      // Start the tween for the value
      tweenedValue.set(currentData.value);
    });

    afterUpdate(() => {
        if (width && height) {
        const currentData = datasets[index];
        const svgElement = `#chart-${index}`;
        createPieChart(currentData, svgElement);
        }
    });
  </script>
  
  <svg id="chart-{index}" width="{width}" height="{height}"></svg>
  <div class="description">{currentData.description}</div>

  <style>
    svg {
      display: block;
      margin: 0 auto;
    }
    .description {
    color: white;
    text-align: center;
    margin-top: 20px;
    font-size: 1em;
  }
  </style>
  