
<script>
    import Graph from '../components/Graph.svelte';
    import Bar from '../components/Bar.svelte';
    import Pie from '../components/Pie.svelte';
    import Pie_2 from '../components/Pie_2.svelte';

    let show = 0;
    let toggle_1 = false;
    let toggle_2 = false;
    let ans;
    let ans_2;

    let index;
    let index2;
    const width = 300;
    const height = 300;
    const width2 = 300;
    const height2 = 300;
    let datasets = [
        { label: 'Share with Family', value: 83, color: '#00a1e4', description: '83% of lottery winners share their jackpot with at least 1 family member.'},
        { label: 'Donate to Charity', value: 40, color: '#ff6384', description: '40% of lottery jackpot winners choose to donate to charity.' },
        { label: 'Buy a Home', value: 66, color: '#ffcd56', description: '66% of lottery winners buy a new home.' },
        { label: 'Vacation Outside U.S.', value: 20, color: '#4bc0c0', description: '20% of lottery winners decide to take a vacation outside the U.S.' }
    ];

    let data = [
      { label: 'Prizes & Jackpots', value: 50, color: '#FF6384' , description: 'Only 50% of all ticket sales go to funding the Powerball prizes and jackpots.'},
      { label: 'Charities', value: 35, color: '#36A2EB', description: '35% of all ticket sales go to causes and charities supported by lotteries across the country.'},
      { label: 'Powerball lottery organisation', value: 9, color: '#FFCE56', description: '9% of ticket sales go to operating expenses of the Powerball lottery organisation.'},
      { label: 'Retailers', value: 6, color: '#4BC0C0', description: '6% of ticket sales go to retailer commissions.'},
    ];

    let toggle_3 = false;
    let toggle_4 = false;

    function update1(text) {
        toggle_1 = true;
        ans = text;
    }

    function update2(text) {
        toggle_2 = true;
        ans_2 = text;
    }

    function response(n) {
        index = n
        toggle_3 = true;
    }

    function updateChart(n) {
        index2 = n
        toggle_4 = true;
    }

    const select_1 = () => update1('Not really...',);
    const select_2 = () => update1('Yes, almost correct!');
    const select_3 = () => update1('Pretty much!');

    const select_4 = () => update2('Good guess!',);
    const select_5 = () => update2("Hmm.. maybe lottery isn't so fair after all");
    const select_6 = () => update2("That's ok, we are here to inform you!");

</script>


<main>
    <br>
    <hr style="width:30%;">
    <br>
    <br>
    <h1>Fun Facts about Powerball</h1>
    <hr style="width:40%">
    <h2 style="text-align: center;">By Kanggun Ham And Jun-Hee Hwang</h2>
    <hr style="width:40%">
    <p style="text-align: center;">
    Welcome to this page where we will explore some POWERBALL statistics!
    <br>
    Answer the questions one by one and explore the visualizations! Enjoy!
    </p>


    <hr style="width:40%;">
    <br>

    <h2>Where Does The Money From The Ticket Sales Go?</h2>
    <p>Click through each options below!</p>
    <div class="btn_group">
        <button on:click={() => updateChart(0)}>(1) Prizes & Jackpots</button>
        <button on:click={() => updateChart(1)}>(2) Charities</button>
        <button on:click={() => updateChart(2)}>(3) Powerball lottery organisation</button>
        <button on:click={() => updateChart(3)}>(4) Retailers</button>
    </div>
    {#if toggle_4}
        <h3>{data[index2].description}</h3>
        <Pie_2 {index2} {width2} {height2}/>

        <p>If <b>50%</b> of the sales goes to Prizes & Jackpots...</p>
        <hr style="width:68%;">
        <br>
        <br>
        
        <h2>How Do Lottery Winners Spend Their Millions?</h2>
        <p>Click through each options below!</p>
        <div class="btn_group">
            <button on:click={() => response(0)}> (1) Share with family </button>
            <button on:click={() => response(1)}> (2) Donate to charity </button>
            <button on:click={() => response(2)}> (3) Buy a home </button>
        </div>
        <br>
    {/if}

    {#if toggle_3} 
        <h3>{datasets[index].description}</h3>
        <Pie {index} {width} {height}/>

        <p>Seems like people like to share their winnings...</p>
        <hr style="width:68%;">
        <br>

        <h2> Which income class do you think participates in lottery the most? </h2>
        <div class="btn_group">
            <button on:click={select_1}> (a) Lower-income </button>
            <button on:click={select_2}> (b) Middle-income </button>
            <button on:click={select_3}> (c) Upper-income </button>
        </div>   
        <br> 
    {/if}

    {#if toggle_1}
        <div class="hide">
            <h3>{ans}</h3>
            <p>The Powerball lottery has a very specific demographic regarding income earners.
                <li>56% of people who make $36,000 and $90,000 annually buy at least one lottery ticket.</li>
                <li>53% of people who make more than $90,000 annually do the same.</li>
                <br>
                And only 40% percent of people how earn less than $36,000 per year buy lottery tickets.
                <br><br>
                Hover over the points to view each state and their median income!
            </p>
        </div>
        <h3>Lottery Sales based on Median Income by states</h3>
        <p style="text-align: center; font-size: 12px;">In Ten Millions of Dollars vs. Median Income</p>
        <Graph />

        <br>
        <br>
        <br>
        <p>People do this regardless of their income..!</p>
        <hr style="width:68%;">
        <br>

        <h2> What do you think the distribution of Powerball winners across states looks like ? </h2>
        <div class="btn_group">
            <button on:click={select_4}> (a) Uneven Distrubution of Winners </button>
            <button on:click={select_5}> (b) Even Distrubution of Winners </button>
            <button on:click={select_6}> (c) I don't know </button>
        </div> 

    {/if}

    <br> 

    {#if toggle_2}
        <div class="hide">
            <h3>{ans_2}</h3>
            <p>
                Random implies that distrubution should be even.
                <b>But</b> the winners seems to come from some <b>specifics states!</b><br>
                <br>
                <li>45 U.S. states and Washington D.C., Puerto Rico, The Virgin Islands have Powerball</li>
                <li>Indiana has the most wins, with a total of 39 Powerball jackpot winners</li>
                <li>But Alabama, Alaska, Hawaii, Nevada, and Utah do not currently have a state lottery.</li>
            </p>
        </div>
        <div class="barchart">
            <div class="text">
                <h3>Number of Jackpot Winners since 1992</h3>
            </div>
            <Bar />
        </div>
        <br>
    {/if}
    <br>



    {#if toggle_1 && toggle_2 && toggle_3}
    <hr style="width:70%;">
    <br>
    <h2> Key Takeaways: </h2>
    <p>
        <li>Most people share their winnings with their loved ones or their community.</li>
        <li>Lower-income individuals does not necessarily purchase more lottery tickets.</li>
        <li>Indiana has the most number of winners since 1992.</li>
        <li>There might be a possibility that certain states are be favored.</li>
    </p>
        
    {/if}

    <br>
    <br>

</main>

<p style="font-size: 13px; text-align: center">
    View our project in <a href='https://github.com/kanggunh/United-States-of-Lottery-Luckiest-States-/tree/main'
    >GitHub</a>
    <br>
    You can watch our website demonstration video <a href="https://youtu.be/tiv2j3dj7Eg">here</a>
    <br>
    References:
    <br>
    <a href="https://www.searchlogistics.com/learn/statistics/powerball-statistics/"
    style="font-size: 10px;">Powerball Statistics & Facts That Will Blow Your Mind</a>
    <br>
    <a href="https://www.justice.gov/ust/eo/bapcpa/20220401/bci_data/median_income_table.htm" 
    style="font-size: 10px;">Median Household Income By States</a>
    <br>
    <a href="https://www.flaticon.com/free-icons/bingo" style="font-size: 10px;">Bingo icons created by Freepik - Flaticon</a>
    <br>
</p>

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
        font-size: 13px;
        color: var(--color-text);
        width: 1200px;
        margin-left: auto;
        margin-right: auto;
        margin-top: 50px;
        background-color: #F3F3F3;
    }
    
    h1 {
        margin-top: -25px;
        font-size: 2em;
        font-weight: 600;
        line-height: 2;
    }

    h2 {
        width: 800px;
        font-size: 14px;
        margin-left: auto;
        margin-right: auto; 
        text-align: left;  
        /* background-color: powderblue; */
    }

    h3 {
        width: 800px;
        font-size: 13px;
        margin-left: auto;
        margin-right: auto; 

        /* background-color: powderblue; */
    }

    p {
        width: 800px;
        margin-left: auto;
        margin-right: auto;
        text-align: left;
        line-height: 2.2;
        font-size: 13px;
    }

    button {
        background-color: #FCFCFC;
        font-family: "Roboto Serif", serif;
        font-size: 11px;
        color: black;
        border: 1.5px solid #1B1717; 
        transition-duration: 0.2s;
        text-align: center;
        border-radius: 5px;
        padding: 15px 25px;
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