<template>
	<div class="space-page">
		<h1 class="space-page__title">Space</h1>

		<div class="space-page__museum-highlights">
			<MuseumHighlight v-for="highlight in paginateHighlights" :highlight="highlight" :key="highlight.id">
				<template v-slot:icon>
					<svg
						width="529"
						height="512"
						viewBox="0 0 529 512"
						fill="currentColor"
						xmlns="http://www.w3.org/2000/svg"
						class="museum-highlight__star"
					>
						<path
							d="M292.9 18C287.6 7 276.4 0 264.1 0C251.8 0 240.7 7 235.3 18L171 150.3L27.4 171.5C15.4 173.3 5.4 181.7 1.7 193.2C-2 204.7 0.999997 217.4 9.6 225.9L113.8 329L89.2 474.7C87.2 486.7 92.2 498.9 102.1 506C112 513.1 125.1 514 135.9 508.3L264.2 439.8L392.5 508.3C403.3 514 416.4 513.2 426.3 506C436.2 498.8 441.2 486.7 439.2 474.7L414.5 329L518.7 225.9C527.3 217.4 530.4 204.7 526.6 193.2C522.8 181.7 512.9 173.3 500.9 171.5L357.2 150.3L292.9 18Z"
							fill="currentColor"
						/>
					</svg>
				</template>

				<template v-slot:extras>
					<a v-if="highlight.quiz" :href="highlight.quiz" class="museum-highlight__body-quiz-link">Take Quiz</a>
				</template>
			</MuseumHighlight>
		</div>

		<button class="space-page__load-more" @click="loadMore" v-if="canLoadMore">
			{{ loading ? "Loading more..." : "Load more" }}
		</button>
	</div>
</template>

<script>
import MuseumHighlight from "./MuseumHighlight";

export default {
	name: "SpacePage",
	components: {
		MuseumHighlight,
	},
	mixins: [],
	props: {},
	data() {
		return {
			spaceHighlights: [
				{
					date: "2020-04-20 12:20:00",
					description:
						"Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.",
					id: 1,
					image: "",
					name: "Asteroids",
				},
				{
					date: "2020-05-20 15:50:00",
					description:
						"A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.",
					id: 9,
					image: "",
					name: "Comets",
				},
				{
					date: "2020-05-01 9:22:00",
					description: "The term planet is ancient, with ties to history, astrology, science, mythology, and religion.",
					id: 7,
					image: "",
					name: "Planets",
					news: {
						date: "2020-08-18 18:00:00",
						title: "Attend our talk about Jupiter with Dr. Hogarth",
					},
					quiz: "https://planetquiz.space",
				},
				{
					date: "2020-07-05 4:10:00",
					description:
						"A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.",
					id: 12,
					image: "",
					name: "Meteor showers",
					news: {
						title: "The Lyrids will peak at on April 21-22 2021, at night",
					},
				},
			],
			spacePartners: {
				observatory: {
					createdAt: "2020-06-01 11:45:00",
					info: "The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.",
					image: "",
					name: "Mauna Kea Observatories",
				},
			},
			initialPage: 1,
			loading: false,
		};
	},
	computed: {
		mapPartnerData() {
			const spacePartnerKeys = Object.keys(this.spacePartners);
			return spacePartnerKeys.map((key) => {
				const partner = this.spacePartners[key];
				return {
					date: partner.createdAt,
					description: partner.info,
					id: new Date(partner.createdAt).toISOString(),
					image: partner.image,
					name: partner.name,
					news: null,
					quiz: null,
					partnerData: true,
				};
			});
		},

		sortedHighlights() {
			return [...this.spaceHighlights, ...this.mapPartnerData].sort(this.sortByDate).reverse();
		},

		paginateHighlights() {
			return [...this.sortedHighlights.slice(0, this.initialPage * 2)];
		},

		canLoadMore() {
			return this.paginateHighlights.length !== this.sortedHighlights.length;
		},
	},
	methods: {
		sortByDate(a, b) {
			return new Date(b.date) - new Date(a.date);
		},

		loadMore() {
			// mimic async call with setTimeout
			this.loading = true;
			setTimeout(() => {
				this.initialPage++;
				this.loading = false;
			}, 500);
		},
	},
	created() {},
};
</script>

<style lang="scss" scoped>
@import "../styles/common";

.space-page {
	max-width: 1000px;
	margin: 24px auto;
	display: flex;
	flex-direction: column;
	gap: 32px;
	padding-inline: 24px;
	padding-top: 70px;
	&__title {
		text-align: left;
		font-family: Fraunces;
		color: $blue;
		/* font-size: 24px; */
		font-weight: 600;
		padding: 0;
		margin: 0;
	}
	&__museum-highlights {
		display: grid;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		gap: 24px;
		@media screen and (max-width: 800px) {
			grid-template-columns: repeat(1, minmax(0, 1fr));
		}
	}
	&__load-more {
		width: 240px;
		margin: 0 auto;
		height: 48px;
		border: none;
		border-radius: 16px;
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
</style>
