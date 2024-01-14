<script lang="ts">
	import {Route, Router} from "svelte-routing";
	import Navbar from "./Navbar.svelte";
	import Home from "./Home.svelte";
	import Team from "./teams/Team.svelte";
	import HomeTuto from "./tutorial/HomeTuto.svelte";
	import CharacterDetails from "./characters/CharacterDetails.svelte";
	import Footer from "./Footer.svelte";

	export let url;

</script>

<Router url="{url}">
	<main>
		<Navbar />
		<div>
			<Route path="/tuto" component="{HomeTuto}" />
			<Route path="/"><Home /></Route>
			<Route path="/team"><Team /></Route>
			<Route path="/character/:name" let:params><CharacterDetails name="{params.name}" /></Route>
		</div>
		<hr />
		<Footer />
	</main>
</Router>

<style>
	main {
		text-align: center;
		max-width: 240px;
		margin: 0 auto;
		padding: 0;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
