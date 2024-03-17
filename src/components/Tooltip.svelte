<script>
    export let data;
    export let xScale;
    export let yScale;

    $: console.log(data.sales_in_million);
    $: console.log(yScale(data.sales_in_million));
    $: console.log(xScale(data.income_two));
</script>



<div class='tooltip' style="position: absolute;
    top: {yScale(data.sales_in_million) + 1770}px;
    left: {xScale(data.income_two) + 400}px;">
    <h1>{data.states} </h1>
    <p> ${Math.round(data.sales_in_million * 100) / 10} million in Sales</p>
    <p>${Math.round(data.income_two * 1) / 1} Median Income</p>
</div>


<style>
    .tooltip {
        padding: 1px;
        font-size: 10px;
        background: white;
        border: 1px solid rgba(0, 0, 0, 0.5);
        pointer-events: none;
        transition: top 300ms ease, left 300ms ease;
        width: 150px;
        margin-left: 100px;
    }

    h1 {
        font-weight: 700;
        margin-bottom: 0.25rem;
        font-size: 13px;
        line-height: 0.5;
        text-align: left;
        padding-left: 10px;
    }

    p {
        line-height: 0.5;
        text-align: left;
        padding-left: 10px;
    }
</style>