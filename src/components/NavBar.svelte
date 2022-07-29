<script>
    import Fa from 'svelte-fa'
    import { faBars } from '@fortawesome/free-solid-svg-icons'
    import { faGithub } from '@fortawesome/free-brands-svg-icons';


    let burgerTruthy = false
    let rotation = 0
    let vh = 0
    let display
    let position
    let height

    let screenWidth = document.documentElement.clientWidth;

    if(screenWidth <= 600) {
        display = "none"
    }  else {
        display = "block"
    }

    const burgerFunc = () => {
        if(burgerTruthy === false) {
            burgerTruthy = true
            rotation = 90
            display = "block"
            height = window.innerHeight - 304
            console.log(height)
            position = "relative"
        } else {
            burgerTruthy = false
            rotation = 0
            display = "none"
            height = 0
            position = "absolute"
        }
    }

    console.log(window.innerHeight)

    

    const resizeFunc = () => {
        screenWidth = document.documentElement.clientWidth
        if(screenWidth <= 600 && burgerTruthy === false) {
            display = "none"
            position = "absolute"
        }  else {
            display = "block"
            burgerTruthy = false
            position = "relative"
        }
    }

    window.addEventListener("resize", resizeFunc)

</script>

<div id="Nav">
<nav>



    <div id="hamburger" class:burgerInvisible={screenWidth > 600} class:burgerVisible={screenWidth <= 600} on:click={burgerFunc}>
        <Fa icon={faBars} scale={3} style="
        margin-top: 30px;
        transform: rotate({rotation}deg);
        color: white;
        transition: 0.5s;
        " />
    </div>
    

    
</nav>


<div id="nav-items"
    style="padding-bottom: {height}px;"
    class:extend={burgerTruthy === true}
    class:retract={burgerTruthy === false}
>


<h1 
   class="nav-item" 
   style="display: {display}; position: {position}">
   About us
</h1>




<h1 
   class="nav-item" 
   style="display: {display}; position: {position}">
   Menu
</h1>




<h1 
   class="nav-item" 
   style="display: {display}; position: {position}">
   Third page
</h1>
</div>

</div>

<style>

    nav {
        position: relative;
        top: 0;
        left: 0;
        background: black;
        padding-bottom: 100px
    }
    
    .extend {
        transition: 0.5s;

    }


    .burger {

    }

    .noBurger {

    }


    /*Character stuff*/

    #nav-items {
        position: absolute;
        display: flex;
        justify-content: center;
        top: 0;
        background: black;
        width: 100%;
    }




    h1 {
        margin: 30px 5%;
        color: white
    }



    /*Burger stuff*/
    #hamburger {
        position: absolute;
        display: none
    }

    .burgerVisible {
        display: block;
        right: 35px
    }




    @media only screen and (max-width: 600px) {
        #hamburger {
            display: block;
            right: 10%;
        }

        #nav-items {
            display: block;
            top: 100px;
            right: 0;
   
            /* height: 87vh; */
            width:20%;
            background: black;
            transition: 0.5s;
        }

        h1 {
            font-size: medium;
        }
    }
</style>