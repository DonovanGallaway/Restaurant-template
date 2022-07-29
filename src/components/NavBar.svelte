<script>
    import Fa from 'svelte-fa'
    import { faBars } from '@fortawesome/free-solid-svg-icons'
    import { faGithub } from '@fortawesome/free-brands-svg-icons';


    let burgerTruthy = false
    let rotation = 0
    let opacity
    //let position
    let height
    let marginTop
    let marginHelper

    let screenWidth = document.documentElement.clientWidth;

    if(screenWidth <= 600) {
        opacity = 0
    }  else {
        opacity = 1

    }

    const burgerFunc = () => {
        if(burgerTruthy === false) {
            burgerTruthy = true
            rotation = 90
            opacity = 1
            height = window.innerHeight - 100
            console.log(height)
            //position = "relative"
            marginTop = 50
            marginHelper = 50
        } else {
            burgerTruthy = false
            rotation = 0
            opacity = 0
            height = 0
            marginTop = 0
            marginHelper = 0
            //position = "absolute"
            
        }
    }

    console.log(window.innerHeight)

    

    const resizeFunc = () => {
        screenWidth = document.documentElement.clientWidth
        if(screenWidth <= 600 && burgerTruthy === false) {
            opacity = 0
            position = "absolute"
        }  else {
            opacity = 1
            marginHelper = 0
            marginTop = 30
            burgerTruthy === true ? burgerFunc() : burgerTruthy = false
            position = "relative"
        }
    }

    window.addEventListener("resize", resizeFunc)

</script>

<div id="Nav">
<nav>



    <div id="hamburger" style="padding: 10px" on:click={burgerFunc}>
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

</div>

<div id="test"></div>
<div id="test2"></div>

<style>

    nav {
        position: relative;
        top: 0;
        left: 0;
        background: black;
        padding-bottom: 100px
    }

    #Nav {
        position: fixed;
        width: 100%;
        z-index: 10;
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
        color: white;
    }



    /*Burger stuff*/
    #hamburger {
        position: absolute;
        display: none
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
   
            width:25%;
            background: black;
            transition: 0.5s;
        }

        h1 {
            font-size: medium;
            position: absolute;
            transition: 0.3s;
        }
    }
</style>