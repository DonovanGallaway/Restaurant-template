<script>
    import Fa from 'svelte-fa'
    import { faBars } from '@fortawesome/free-solid-svg-icons'
    import { fade, blur, fly, slide, scale, crossfade } from 'svelte/transition';
    import { faGithub } from '@fortawesome/free-brands-svg-icons';


    let burgerTruthy = false
    let rotation = 0
    let opacity
    //let position
    let height = document.documentElement.clientHeight * 0.90
    let marginTop
    let marginHelper
    let position
    let burgerSize = 3

    let navBar = false

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
            //height = window.innerHeight
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
    }

    window.addEventListener("resize", resizeFunc)

</script>

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
        <h1 class="nav-item">About us</h1>
        <h1 class="nav-item">Menu</h1>
        <h1 class="nav-item">another page</h1>
    </div>

    {/if}

</nav>


</div>

{#if burgerTruthy}
    <div class="burgerContent" transition:fly={{y: -height, duration: 500, opacity: 1}}>
        <h3 on:click={() => console.log('about me was clicked')} class="hambuger-item">About me</h3>
        <h3 class="hambuger-item">menu</h3>
        <h3 class="hambuger-item">Another page</h3>
    </div>
{/if}



<style>

    #stickyNav {
        position: fixed;
        width: 100%;
        z-index: 5;
    }

    nav {
        position: relative;
        top: 0;
        left: 0;
        background: black;
        padding-bottom: 15vh;
        z-index: 2;
    }

    .nav-items {
        position: absolute;
        display: flex;
        top: 50%;
        transform: translateY(-50%);
        width: 100%;
    }

    .nav-item {
        color: white;
        display: inline;
        margin: auto;
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

    .hambuger-item {
        color: white;
        margin: 5px;
        margin-top: 20px;
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
        top: 100px;
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
    }
</style>


<!--<div id="nav-items"
    
    style="padding-bottom: {height}px;"
>


<h1 
   class="nav-item" 
   
   style="
    opacity: {opacity};
    margin-top: {marginTop}px
   ">
   About us
</h1>




<h1 
   class="nav-item" 
   style="opacity: {opacity};
   margin-top: {marginTop + marginHelper}px
   ">
   Menu
</h1>




<h1 
   class="nav-item" 
   style="opacity: {opacity};
   margin-top: {marginTop + marginHelper * 2}px
   ">
   Third page
</h1>
</div>

</div>-->