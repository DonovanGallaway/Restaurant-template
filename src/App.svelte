<script>
	import NavBar from "./components/NavBar.svelte";
	import Footer from "./components/Footer.svelte";

	import AboutUs from "./components/Pages/AboutUs.svelte";
	import Menu from "./components/Pages/Menu.svelte";
	import ContactUs from "./components/Pages/ContactUs.svelte";

	const tabs = ['about us', 'menu', 'contact us']

	let currentTab = 'about us'
</script>

<NavBar {tabs} on:tabChange={(e) => {
	currentTab = undefined
	currentTab = e.detail
	// setTimeout(() => {
	// 	currentTab = e.detail
	// }, 500);
	console.log(currentTab)
}}/>

<!--<div id="navBar-space"></div>-->

<main>
	{#if currentTab === 'about us'}
		<AboutUs />
	{/if}

	{#if currentTab === 'menu'}
		<Menu />
	{/if}

	{#if currentTab === 'contact us'}
	<ContactUs />
	{/if}
</main>

<Footer />

<style>
	main {
		position: relative;
		height: 100%;
		width: 100%;
	}
</style>