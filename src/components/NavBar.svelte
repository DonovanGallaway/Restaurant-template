<script>
    import Fa from 'svelte-fa'
    import { faBars } from '@fortawesome/free-solid-svg-icons'
    import { fade, blur, fly, slide, scale, crossfade } from 'svelte/transition';
    import { faGithub } from '@fortawesome/free-brands-svg-icons';
    import { createEventDispatcher } from 'svelte'


    const dispatch = createEventDispatcher()

    export let tabs

    let burgerTruthy = false
    let rotation = 0
    let height = document.documentElement.clientHeight * 0.90
    let burgerSize = 3
    let navBar = false
    let currentTab = 'about us'

    let screenWidth = document.documentElement.clientWidth;

    if(screenWidth <= 600) {
        navBar = true
    }  else {
        navBar = false

    }

    if(document.documentElement.clientHeight <= 500) {
        burgerSize = 2
    }  

    const burgerFunc = () => {
        if(burgerTruthy === false) {
            burgerTruthy = true
            rotation = 90
            console.log(height)
        } else {
            burgerTruthy = false
            rotation = 0
        }
    }

    console.log(document.documentElement.clientHeight * 0.65)

    

    const resizeFunc = () => {
        screenWidth = document.documentElement.clientWidth
        if(screenWidth <= 600 && burgerTruthy === false) {
            navBar = true
        }  else {
            navBar = false
            burgerTruthy === true ? burgerFunc() : burgerTruthy = false
        }

        if(document.documentElement.clientHeight <= 500) {
            burgerSize = 2
        } else {
            burgerSize = 3
        }
    }

    window.addEventListener("resize", resizeFunc)

</script>


<!--<div id="navSpace">-->
<div id="stickyNav">
    <nav>


        {#if navBar}
        <div id="hamburger" style="padding: 10px" on:click={burgerFunc}>
            <Fa icon={faBars} scale={burgerSize} style="
                transform: rotate({rotation}deg);
                color: white;
                transition: 0.5s;
            " />
        </div>

        {:else}
        <div class="nav-items">

            {#each tabs as tab}
                <div class="nav-item-container">
                    <h1 class:chosenTab={currentTab ===tab} class="nav-item" on:click={() => {
                        currentTab = tab
                        dispatch('tabChange', tab)
                    }}>{tab}</h1>
                </div>
            {/each}
        </div>

        {/if}

    </nav>


</div>
<!--</div>-->

{#if burgerTruthy}
    <div class="burgerContent" transition:fly={{y: -height, duration: 500, opacity: 1}}>

        {#each tabs as tab}
            <h3 on:click={() => dispatch('tabChange', tab)} class="hamburger-item">{tab}</h3>
        {/each} 
    </div>
{/if}

<!--<div id="test"></div>
<div id="test2"></div>-->

<style>

    #navSpace {
        position: relative;
        top: 0;
        left: 0;
        padding-bottom: 10vh;
    }

    #stickyNav {
        position: sticky;
        top: 0;
        width: 100%;
        z-index: 5;
    }

    nav {
        position: relative;
        top: 0;
        left: 0;
        background: black;
        padding-bottom: 10vh;
        z-index: 2;
    }

    .nav-items {
        position: absolute;
        display: flex;
        top: 50%;
        transform: translateY(-50%);
        width: 100%;
        cursor: pointer;
    }

    .nav-item-container {
        margin: auto; 
        display: inline; 
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .nav-item {
        position: absolute;
        color: white;
        display: inline;
        margin: auto;
        transition: 0.1s;
    }

    .chosenTab {
        font-size: 35px;
        color:rgb(112, 130, 233)
    }

    .nav-item:hover {
        color: rgb(150, 148, 148)
    }

    .nav-item:active {
        font-size: 20px
    }

    .burgerContent {
        position: fixed;
        margin-top: 20%;
        width: 25%;
        height: 85vh;
        bottom: 0;
        background: black;
        right: 0;
        z-index: 1;
    }

    .hamburger-item {
        color: white;
        margin: 5px;
        margin-top: 20px;
        cursor: pointer;
    }

    /*Burger stuff*/
    #hamburger {
        position: absolute;
        display: none;
        top: 50%;
        transform: translateY(-50%);
        margin: 0;
        z-index: 2;
    }


    #test {
        position: relative;
        padding-bottom: 200vh;
        width: 100%;
        background: pink;

    }

    #test2 {
        width: 100%;
        height: 20vh;
        background-color: blue;
    }


    @media only screen and (max-width: 600px) {

        nav {
            padding-bottom: 15vh;
        }
        
        #navSpace {
            padding-bottom: 15vh;
        }

        #hamburger {
            display: block;
            right: 7%;
        }
    }

    
    @media only screen and (max-width: 400px) {
        .burgerContent {
            width: 40%;
        }

        #hamburger {
            right: 14%
        }
    }

    @media only screen and (max-height: 500px) { 
        nav {
            padding-bottom: 70px
        }

        #navSpace {
            padding-bottom: 70px;
        }
    }
</style>
