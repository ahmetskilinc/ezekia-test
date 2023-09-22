<template>
	<nav class="navbar">
		<div class="navbar__wrapper">
			<p class="navbar__wrapper-logo">Natural History Museum</p>
			<button class="navbar__wrapper-menu-button" @click="doButton">
				<svg width="18" height="12" viewBox="0 0 18 12" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
					<path
						d="M1 12C0.716667 12 0.479167 11.9042 0.2875 11.7125C0.0958333 11.5208 0 11.2833 0 11C0 10.7167 0.0958333 10.4792 0.2875 10.2875C0.479167 10.0958 0.716667 10 1 10H17C17.2833 10 17.5208 10.0958 17.7125 10.2875C17.9042 10.4792 18 10.7167 18 11C18 11.2833 17.9042 11.5208 17.7125 11.7125C17.5208 11.9042 17.2833 12 17 12H1ZM1 7C0.716667 7 0.479167 6.90417 0.2875 6.7125C0.0958333 6.52083 0 6.28333 0 6C0 5.71667 0.0958333 5.47917 0.2875 5.2875C0.479167 5.09583 0.716667 5 1 5H17C17.2833 5 17.5208 5.09583 17.7125 5.2875C17.9042 5.47917 18 5.71667 18 6C18 6.28333 17.9042 6.52083 17.7125 6.7125C17.5208 6.90417 17.2833 7 17 7H1ZM1 2C0.716667 2 0.479167 1.90417 0.2875 1.7125C0.0958333 1.52083 0 1.28333 0 1C0 0.716667 0.0958333 0.479167 0.2875 0.2875C0.479167 0.0958333 0.716667 0 1 0H17C17.2833 0 17.5208 0.0958333 17.7125 0.2875C17.9042 0.479167 18 0.716667 18 1C18 1.28333 17.9042 1.52083 17.7125 1.7125C17.5208 1.90417 17.2833 2 17 2H1Z"
						fill="currentColor"
					/>
				</svg>
			</button>
		</div>
	</nav>
</template>

<script>
export default {
	name: "Navbar",
	methods: {
		doButton() {
			alert("Menu should open but we don't have one, yet.");
		},
	},
};
</script>

<style lang="scss" scoped>
@import "../styles/common";

.navbar {
	position: fixed;
	z-index: 999;
	top: 0;
	left: 0;
	right: 0;
	font-family: Fraunces;
	background: $blue;
	height: 70px;
	&__wrapper {
		width: 100%;
		height: 100%;
		max-width: 1000px;
		display: flex;
		margin: 0 auto;
		align-items: center;
		justify-content: space-between;
		padding-inline: 24px;
		&-logo {
			color: $white;
			font-size: 20px;
		}
		&-menu-button {
			cursor: pointer;
			border: none;
			height: 32px;
			width: 32px;
			background: transparent;
			color: $white;
			border-radius: 5px;
			transition: all 500ms;
			box-shadow: none;
			&:hover {
				background-color: darken($blue, 10%);
				box-shadow: 0px 17px 56px -24px rgba(128, 128, 0, 0.55);
			}
		}
	}
}
</style>
