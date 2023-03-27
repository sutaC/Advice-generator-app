<script>

    import { onMount } from "svelte";

    let advice = null;

    
    const rolladvice = async () => {
        
        advice = null;
        
        try {

            const response = await fetch('https://api.adviceslip.com/advice');
            advice = await response.json();

        } catch (error) {

            console.error(error);
            advice = 'error';

        }
        
    };
    
    onMount(rolladvice())

</script>
<!-- ---  -->


<main> 

    {#if advice === null}

        <h1>ADVICE ...</h1>
        
        <p>Waiting...</p>  
    
    {:else if advice === 'error'}
        
        <h1>ADVICE ...</h1>
            
        <p>Error occurred!</p>

    {:else}
        
        <h1>ADVICE #{advice.slip.id}</h1>

        <p>"{advice.slip.advice}"</p>

    {/if}

    <div class="devider"></div>

    <button 
        aria-label="Roll advice"
        
        on:click={() => rolladvice()}
    ></button>

</main>


<!-- ---  -->
<style>
    @import url('https://fonts.googleapis.com/css2?family=Manrope:wght@800&display=swap');  
    
    :root {

        font-family: 'Manrope', sans-serif;
        font-size: 28px;

        /* Primary */
        --clr-light-cyan: hsl(193, 38%, 86%);
        --clr-neon-green: hsl(150, 100%, 66%);

        /* Neutral */
        --clr-grayish-blue: hsl(216, 19%, 38%);
        --clr-dark-grayish-blue: hsl(217, 19%, 24%);
        --clr-dark-blue: hsl(218, 23%, 16%);
    }

    /* Mian styles */

    :global(body) {
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        
        box-sizing: border-box;
        margin: 0;
        min-height: 100vh;
        
        padding: 0.5rem;
        
        background-color: var(--clr-dark-blue);
    }

    
    main {
        max-width: 15rem;

        padding: 1rem 0.8rem 0rem 0.8rem;

        border-radius: 1rem;

        background-color: var(--clr-dark-grayish-blue);
        box-shadow: 0px 0px 0.15rem var(--clr-grayish-blue);

    }
    
    .devider {
        height: 1rem;

        background-image: url('/pattern-divider-mobile.svg');
        background-repeat: no-repeat;
        background-position: center;
    }


    h1 {
        color: var(--clr-neon-green);
        font-size: 0.4rem;
        letter-spacing: 0.1rem;
    }

    p {

        font-size: 0.8rem;
        color: var(--clr-light-cyan);
    }

    button {
        height: 0.5em;
        width: 0.5rem;

        padding: 0.95rem;

        border: none;
        border-radius: 100%;
        
        background-color: var(--clr-neon-green);
        background-image: url('/icon-dice.svg');
        background-repeat: no-repeat;
        background-position: center;

        transform: translate(0, 1rem);
    }

    button:active {
        box-shadow: 0px 0px 1rem var(--clr-neon-green);
    }
    
    
    @media (min-width: 400px) {

        .devider {
            background-image: url('/pattern-divider-desktop.svg');
        }

    }
    

</style>