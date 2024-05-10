<template>
	<main>
		<h1 class="text-center">Movies</h1>
		<div class="d-flex flex-wrap">
			<CardMovie v-for="movie in store.movies" :movie="movie" />
		</div>
		<h1 class="text-center">Tv series</h1>
		<div class="d-flex flex-wrap">
			<CardSerie  v-for="tvSerie in store.series" :tvSerie="tvSerie"/>
		</div>
	</main>
</template>

<script>
import { store } from "../store";
import CardMovie from "./CardMovie.vue";
import CardSerie from "./CardSerie.vue";

export default {
	components: {
		CardMovie,
		CardSerie,
	},
	data() {
		return {
			store,
		};
	},
	methods: {},
};
</script>

<style lang="scss">
main {
	height: calc(100vh - 80px);
	background-color: #434343;
	overflow-y: auto;
	color: white;
	.my-card {
		cursor: pointer;
		width: 342px;
		height: 513px;
		perspective: 1000px;
		.flip-card-inner {
			position: relative;
			width: 100%;
			height: 100%;
			text-align: center;
			transition: transform 0.8s;
			transform-style: preserve-3d;
		}
		&:hover .flip-card-inner {
			transform: rotateY(180deg);
		}
		.front-card,
		.back-card {
			position: absolute;
			width: 100%;
			height: 100%;
			-webkit-backface-visibility: hidden; /* Safari */
			backface-visibility: hidden;
		}
		.back-card {
			background-color: black;
			transform: rotateY(180deg);
		}
		.flag-img {
			width: 25px;
			img {
				width: 100%;
			}
		}
		img {
			max-width: 100%;
			min-height: 100%;
			object-fit: cover;
		}
	}
}
</style>
