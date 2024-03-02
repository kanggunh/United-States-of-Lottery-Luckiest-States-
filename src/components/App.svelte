
<script>
    import Graph from '../components/Graph.svelte';
    import Bar from '../components/Bar.svelte';
    import Pie from '../components/Pie.svelte';

    let show = 0;
    let toggle_1 = false;
    let toggle_2 = false;
    let ans;

    let index = 0;
    const width = 300;
    const height = 300;
    let datasets = [
        { label: 'Share with Family', value: 83, color: '#00a1e4', description: '83% of lottery winners share their jackpot with at least 1 family member.' },
        { label: 'Donate to Charity', value: 40, color: '#ff6384', description: '40% of lottery jackpot winners choose to donate to charity.' },
        { label: 'Buy a Home', value: 66, color: '#ffcd56', description: '66% of lottery winners buy a new home.' },
        { label: 'Vacation Outside U.S.', value: 20, color: '#4bc0c0', description: '20% of lottery winners decide to take a vacation outside the U.S.' }
    ];

    function update1(text) {
        toggle_1 = true;
        ans = text;
    }

    function update2(text) {
        toggle_2 = true;
        ans = text;
    }

    function response(n) {
        index = n
    }

    const select_1 = () => update1('Not really...',);
    const select_2 = () => update1('Yes, almost correct!');
    const select_3 = () => update1('Pretty much!');

</script>


<main>
    <h1>Fun Facts about Powerball</h1>
    <h2>How Do Lottery Winners Spend Their Millions?</h2>
    <div class="facts">
        <button on:click={() => response(0)}> (1) Share with family </button>
        <button on:click={() => response(1)}> (2) Donate to charity </button>
        <button on:click={() => response(2)}> (3) Buy a home </button>
        <button on:click={() => response(3)}> (4) Vacation outside the U.S. </button>
    </div>
    <h3>{datasets[index].description}</h3>
    <Pie {index} {width} {height}/>
    <h1>Scatterplot</h1>

    <h2> Which income class do you think participates in lottery the most? </h2>
    <div class="btn_group">
        <button on:click={select_1}> (a) Lower-income </button>
        <button on:click={select_2}> (b) Middle-income </button>
        <button on:click={select_3}> (c) Upper-income </button>
    </div>   
    <br> 
    {#if toggle_1}
        <div class="hide">
            <h3>{ans}</h3>
            <p>The Powerball lottery has a very specific demographic regarding income earners.
                <li>56% of people who make $36,000 and $90,000 annually buy at least one lottery ticket.</li>
                <li>53% of people who make more than $90,000 annually do the same.</li>
                <br>
                And only 40% percent of people how earn less than $36,000 per year buy lottery tickets.
            </p>
        </div>
        <h3>Lottery Sales based on Median Income by states</h3>
        <p style="text-align: center; font-size: 12px;">In Ten Millions of Dollars vs. Median Income</p>
        <Graph />
        <br>
    {/if}

    {#if toggle_2}
        <div class="hide">
            <h3>{ans}</h3>
            <p>The Powerball lottery has a very specific demographic regarding income earners.
                <li>56% of people who make $36,000 and $90,000 annually buy at least one lottery ticket.</li>
                <li>53% of people who make more than $90,000 annually do the same.</li>
                <br>
                And only 40% percent of people how earn less than $36,000 per year buy lottery tickets.
            </p>
        </div>
        <Bar />
        <br>
    {/if}
    <br>

    <p> Write up: <br>
        So far we have a have a button that let's user guess their intuitions before showing the real data. Doing so promotes self reflection
        and makes the user think before mindlessly viewing the visualization. 
        At the moment, we are planning to use 'scrollytelling' to first show the above pie charts then let the 
        user explore other data at the end with scatterplots and barcharts about the powerball. The most challenging part will 
        be to implement the scrolling and animating the pie chart to move along with the scroll. We are currently done making pie charts
        on our local device but unable to make it work on github.

    <br>
    <br>
    <a href="https://www.flaticon.com/free-icons/bingo" title="bingo icons" style="font-size: 10px;">Bingo icons created by Freepik - Flaticon</a>
</main>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Protest+Strike&display=swap');
    @import url('https://fonts.googleapis.com/css2?family=Roboto+Serif:ital,opsz,wght@0,8..144,100..900;1,8..144,100..900&display=swap');

    :root {
        --color-bg: #ffffff;
        --color-outline: #c2c2c2;
        --color-shadow: hsl(0, 0%, 0%, 0.1);
        --color-text: #3f4252;
        --color-bg-1: hsla(0, 0%, 0%, 0.2);
        --color-shadow-1: hsl(0, 0%, 96%);
        background-color: #FCFCFC;
    }

    main {
        text-align: center;
        font-family: "Roboto Serif", serif;
        font-style: normal;
        font-weight: 400;
        font-size: 15px;
        color: var(--color-text);
        width: 1000px;
        margin-left: auto;
        margin-right: auto;
        margin-top: 50px;
        background-color: #F3F3F3;
    }

    h1 {
        margin-top: -25px;
        font-size: 3em;
        font-weight: 600;
        line-height: 2;
    }

    h2 {
        width: 800px;
        font-size: 16px;
        margin-left: auto;
        margin-right: auto; 
        text-align: left;  
        /* background-color: powderblue; */
    }

    p {
        width: 800px;
        margin-left: auto;
        margin-right: auto;
        text-align: left;
        line-height: 2.2;
        font-size: px;
    }

    button {
        background-color: #FCFCFC;
        font-family: "Roboto Serif", serif;
        font-size: 13px;
        color: black;
        border: 1.5px solid #1B1717; 
        transition-duration: 0.2s;
        text-align: center;
        border-radius: 5px;
        padding: 15px 28px;
        margin-top: 5px;
        margin-bottom: 5px;
        font-weight: 500;
    }

    button:hover {
        background-color: #d3d3d3; 
        color: white;
    }

    button:active {
        background: #2e2e2e;
        border: 1.5px solid black;
        color: white;
    }

    h2 {
        width: 800px;
        margin-left: auto;
        margin-right: auto; 
        text-align: left;
    }

    div.btn_group {
        width: 800px;
        text-align: left;
        margin-left: auto;
        margin-right: auto;
    }

    div.hide {
        width: 800px;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 50px;
        text-align: left;
        /* background-color: powderblue; */
    }
</style>
