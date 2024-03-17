<script>
    export let data;
    export let xScale;
    export let yScale;
</script>

<div class='tooltip' style="position: absolute;
  top: {yScale(data.state) + 2750}px;
  left: 800px">
<h1>{data.state}</h1> 
<p>{data.count} Winners</p>
</div>

<style>
    .tooltip {
      position: relative;
      display: inline-block;
      padding-left: 12px;
      padding-right: 12px;
      padding-top: 1px;
      padding-bottom: 1px;
      background: #FFFFFF;
      border: 0.1px solid rgba(0, 0, 0, 0.5);
      pointer-events: none;
      transition: opacity 1s;
      /* transition: top 300ms ease, left 300ms ease; */
    }
  
    h1 {
      font-size: 13px;
      font-weight: 500;
      margin-bottom: 0.1rem;
    }

    p {
        font-size: 10px;
        font-weight: 400;
        margin-bottom: 0.3rem;
    }

  </style>