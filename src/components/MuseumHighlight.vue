<template>
	<div class="museum-highlight" :style="{ backgroundColor: partnerDataBackground }">
		<div class="museum-highlight__image" :style="{ background: `url(${image})` }"></div>
		<div class="museum-highlight__body">
			<h1 class="museum-highlight__body-title">{{ highlight.name }}</h1>
			<p class="museum-highlight__body-description" :style="{ flexGrow: !highlight.news && !highlight.quiz ? 1 : 0 }">
				{{ highlight.description }}
			</p>
			<!-- <p class="museum-highlight__body-date" :style="{ flexGrow: !highlight.news && !highlight.quiz ? 1 : 0 }" v-if="highlight.date">
				{{ formatDate(highlight.date) }}
			</p> -->
			<div class="museum-highlight__body-news" v-if="highlight.news" :style="{ flexGrow: !highlight.quiz ? 1 : 0 }">
				<p>{{ highlight.news.title }}{{ getNewsDate }}</p>
			</div>
			<slot name="extras" />
			<button class="museum-highlight__body-cta" @click="refreshImage"> Refresh image </button>
		</div>
		<slot name="icon" />
	</div>
</template>

<script>
import { format } from "date-fns";

export default {
	name: "MuseumHighlight",
	props: {
		highlight: {},
	},
	data() {
		return {
			image: "https://source.unsplash.com/random?planets",
		};
	},
	computed: {
		getNewsDate() {
			if (!this.highlight.news.date) return null;
			const date = new Date(this.highlight.news.date);
			return `, ${format(date, "MMMM d yyyy")}`;
		},
		partnerDataBackground() {
			return this.highlight.partnerData ? "pink" : "";
		},
	},
	methods: {
		// Keywords to get image from fake image api
		getNewKeyword() {
			const keywords = ["space", "earth", "technology", "programming", "fun", "work", "cars", "formula%20one"];
			return keywords[Math.floor(Math.random() * keywords.length)];
		},
		// Fake image api
		refreshImage() {
			this.image = `https://source.unsplash.com/random?${this.getNewKeyword()}`;
		},
		formatDate(date) {
			console.log(date);
			const newDate = new Date(date);
			return format(newDate, "MMMM d yyyy");
		},
	},
};
</script>

<style lang="scss" scoped>
@import "../styles/common";

.museum-highlight {
	margin: 0 auto;
	border-radius: 24px;
	display: grid;
	grid-template-rows: repeat(2, minmax(0, 1fr));
	color: $grey;
	background-color: $white;
	position: relative;
	width: 100%;
	box-shadow: 0px 18px 56px -26px rgba(0, 0, 0, 0.59);
	transition: all 300ms;
	&:hover {
		box-shadow: 0px 40px 50px -36px rgba(0, 0, 0, 0.59);
		transform: scale(1.01);
		z-index: 998;
	}
	&__star {
		position: absolute;
		top: -10px;
		right: -10px;
		height: 32px;
		width: 32px;
		color: #ffff00;
		box-shadow: 0px 17px 56px -24px rgba(128, 128, 0, 0.55);
	}
	&__image {
		background-size: cover;
		background-position: center;
		width: 100%;
		max-height: 100%;
		border-radius: 24px 24px 0 0;
	}
	&__body {
		display: flex;
		flex-direction: column;
		font-family: Montserrat;
		&-title {
			font-family: Fraunces;
			margin-top: 0;
			margin-bottom: 18px;
			color: $dark-blue;
			font-size: 26px;
		}
		&-description {
			font-size: 16px;
			line-height: 1.3;
			margin-bottom: 18px;
		}
		&-news {
			margin-bottom: 18px;
		}
		&-date {
			margin-bottom: 18px;
		}
		&-quiz-link {
			margin-bottom: 18px;
			flex-grow: 1;
		}
		&-cta {
			width: 100%;
			height: 48px;
			border: none;
			border-radius: 14px;
			background-color: $blue;
			cursor: pointer;
			font-family: Montserrat;
			color: $white;
			transition: all 500ms;
			&:hover {
				background-color: darken($blue, 10%);
			}
		}
	}
	&__body,
	&__image {
		max-width: 100%;
		padding: 24px;
	}
}
</style>
