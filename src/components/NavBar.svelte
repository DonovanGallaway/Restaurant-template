<script>
    import Fa from 'svelte-fa'
    import { faBars } from '@fortawesome/free-solid-svg-icons'
    import { faGithub } from '@fortawesome/free-brands-svg-icons';


    let burgerTruthy = false
    let rotation = 0

    let screenWidth = document.documentElement.clientWidth;

    const burgerFunc = () => {
        if(burgerTruthy === false) {
            burgerTruthy = true
            rotation = 90
        } else {
            burgerTruthy = false
            rotation = 0
        }
    }

    window.addEventListener("resize", () => {screenWidth = document.documentElement.clientWidth})

    console.log(screenWidth)

</script>

<nav>

    <div id="nav-items"
     class:burger={screenWidth <= 600}
     class:noBurger={screenWidth > 600}
     >


    <h1 
        class="nav-item" 
        class:hidden={screenWidth <= 600 && burgerTruthy === false}
        class:visible={screenWidth <= 600 && burgerTruthy}
        >About us
    </h1>




    <h1 
        class="nav-item" 
        class:hidden={screenWidth <= 600 && burgerTruthy === false}
        class:visible={screenWidth <= 600 && burgerTruthy}
        >Menu
    </h1>




    <h1 
        class="nav-item" 
        class:hidden={screenWidth <= 600 && burgerTruthy === false}
        class:visible={screenWidth <= 600 && burgerTruthy}
        >Third page
    </h1>



    <div id="hamburger" class:burgerInvisible={screenWidth > 600} class:burgerVisible={screenWidth <= 600} on:click={burgerFunc}>
        <Fa icon={faBars} scale={3} style="
        margin-top: 25px;
        transform: rotate({rotation}deg);
        color: white;
        transition: 0.5s;
        " />
    </div>
    </div>

    
</nav>

<style>
    nav {
        position: relative;
        top: 0;
        left: 0;
        background: black;
        padding-bottom: 100px
    }

    .noItems {
        padding-bottom: 70px;
    }

    #nav-items {
        position: absolute;
    }

    .nav-item {
        
    }

    .burger {

    }

    .noBurger {
        display: flex;
        justify-content: center;
        width: 100%;
    }

    .item-container {
        display: block;
    }

    h1 {
        margin: 20px;
        margin-left: 5%;
        margin-right: 5%;
        color: white
    }

    .burgerInvisible {
        position: absolute;
        right: 10%;
        opacity: 0
    }

    .burgerVisible {
        display: block
    }

    .hidden {
        opacity: 0
    }


    @media only screen and (max-width: 600px) {
        /*#hamburger {
            display: block;
            position: absolute;
            right: 10%;
        }

        .nav-item {
            display: none
        }

        nav {
            padding-bottom: 70px
        }*/
    }
</style>