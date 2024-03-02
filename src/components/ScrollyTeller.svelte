<script>
    import Scroller from "@sveltejs/svelte-scroller";
  
    let count, index, offset, progress;
    let visibility={Close: false};

    function onClick() {
        visibility.Close = !visibility.Close;
    }
</script>

<Scroller
  top={0.0}
  bottom={1}
  threshold={0.5}
  bind:count
  bind:index
  bind:offset
  bind:progress
>
    <div class="background" slot="background">
        
    </div>


    <div class="foreground" slot="foreground">

        <div class=button>
            {#if visibility.Close}
                <button on:click={onClick}> Close Tab </button>
                <div class="description">
                    <p>
                        Our goal is to explore the correlation between household income and the sales of lottery tickets in each state.
                        We are currently still brainstorming with what kind of narrative to use in order to effectively present insights
                        to the users of the web page. We will first present users with the general household income and then lottery ticket
                        sales so that users can get a gist of what the trend is before getting hands-on into exploring the data themselves.
                    </p>
                </div> 
            {:else}
                <button on:click={onClick}> Open Tab </button>
            {/if}
        </div>
        <section>Amazing first finding.</section>
        <div class=button>
            {#if visibility.Close}
                <button on:click={onClick}> Close Tab </button>
                <div class="description">
                    <p>
                        Our goal is to explore the correlation between household income and the sales of lottery tickets in each state.
                        We are currently still brainstorming with what kind of narrative to use in order to effectively present insights
                        to the users of the web page. We will first present users with the general household income and then lottery ticket
                        sales so that users can get a gist of what the trend is before getting hands-on into exploring the data themselves.
                    </p>
                </div> 
            {:else}
                <button on:click={onClick}> Open Tab </button>
            {/if}
        </div>
        <section>Awesome second finding.</section>
        <div class=button>
            {#if visibility.Close}
                <button on:click={onClick}> Close Tab </button>
                <div class="description">
                    <p>
                        Our goal is to explore the correlation between household income and the sales of lottery tickets in each state.
                        We are currently still brainstorming with what kind of narrative to use in order to effectively present insights
                        to the users of the web page. We will first present users with the general household income and then lottery ticket
                        sales so that users can get a gist of what the trend is before getting hands-on into exploring the data themselves.
                    </p>
                </div> 
            {:else}
                <button on:click={onClick}> Open Tab </button>
            {/if}
        </div>
        <section>Crazy last finding.</section>
    </div>
</Scroller>

<style>
    .button {
        position: absolute;
        width:20%;
        margin: 5px;
        outline: rgb(150, 51, 51) 3px;
    }
    .background {
      width: 100%;
      height: 100vh;
      position: relative;
      outline: green solid 3px;
    }
  
    .foreground {
      width: 100%;
      margin: 0 auto;
      height: auto;
      position: relative;
      outline: red solid 3px;
    }
  
    .description {
      position: absolute;
      width:100%;
      background: rgba(170, 51, 120, 0.2) /*  40% opaque */;
      margin: 5px;
      outline: black 3px;
      visibility: visible;
    }
  
    section {
      height: 80vh;
      background-color: rgba(0, 0, 0, 0.2); /* 20% opaque */
      /* color: white; */
      outline: magenta solid 3px;
      text-align: center;
      max-width: 1250px;
      color: black;
      padding: 1em;
      margin: 0 0 2em 0;
    }
  </style>