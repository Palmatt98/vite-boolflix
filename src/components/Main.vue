<template>
	<main>
		<h1 class="text-center">Movies</h1>
		<div class="d-flex flex-wrap">
			<CardMovie
				v-for="movie in store.movies"
				@mouseenter="getCastAndGenre('movie', movie.id)"
				@mouseleave="resetCastAndGenre"
				:movie="movie"
				:cast="castArray"
				:genres="genreArray"
			/>
		</div>
		<h1 class="text-center">Tv series</h1>
		<div class="d-flex flex-wrap">
			<CardSerie @mouseenter="getCastAndGenre('tv')" v-for="tvSerie in store.series" :tvSerie="tvSerie" />
		</div>
	</main>
</template>

<script>
import { store } from "../store";
import CardMovie from "./CardMovie.vue";
import CardSerie from "./CardSerie.vue";
import axios from "axios";

export default {
	components: {
		CardMovie,
		CardSerie,
	},
	data() {
		return {
			store,
			baseURL: "https://api.themoviedb.org/3/",
			castArray: [],
			genreArray: [],
		};
	},
	methods: {
		getCastAndGenre(cardType, id) {
			axios
				.get(this.baseURL + cardType + "/" + id + "?append_to_response=credits&api_key=" + store.apiKey)
				.then((response) => {
					const cast = response.data.credits.cast;
					for (let i = 0; i < 5; i++) {
						this.castArray.push(cast[i]);
					}
					console.log("this.castArray:", this.castArray);
					this.genreArray = response.data.genres;
					console.log("this.genreArray:", this.genreArray);
				});
		},
		resetCastAndGenre() {
			this.castArray = [];
			this.genreArray = [];
		},
	},
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
