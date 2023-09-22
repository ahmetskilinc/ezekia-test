<template>
	<div>
		<Navbar />
		<SpacePage />
	</div>
</template>

<script>
import SpacePage from "./components/SpacePage";
import Navbar from "./components/Navbar";

export default {
	name: "App",
	components: {
		SpacePage,
		Navbar,
	},
};
</script>

<style lang="scss">
body {
	background-color: #fef1f3;
}
</style>
