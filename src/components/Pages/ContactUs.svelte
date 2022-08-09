<script>
    import { fade, blur, fly, slide, scale, crossfade } from 'svelte/transition';

    let screenWidth = document.documentElement.clientWidth;
</script>


<div id="container" in:fly={{x: screenWidth, duration: 500, opacity: 1}}
    out:fly={{x: -screenWidth, duration: 500, opacity: 1}}
>
    <h1>Contact us</h1>
    <div id=content></div>
</div>


<style>

    #container {
        position: absolute;
        height: 100%;
        width: 100%;
        background: lightskyblue;
    }

    #content {
        position: relative;
        height: 100%;
        width:100%;
        background: pink;
    }
</style>