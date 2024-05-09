<template>
	<main>
		<h1 class="text-center">Movies</h1>
		<div class="d-flex flex-wrap">
			<div class="my-card m-5" v-for="movie in store.movies">
				<div class="flip-card-inner">
					<div class="front-card">
						<img v-if="movie.poster_path !== null" :src="URLImage + movie.poster_path" alt="" />
						<img v-else class="placeholder-img" :src="getPlaceholderImg()" alt="" />
					</div>
					<div class="back-card p-5">
						<p>Titolo: {{ movie.title }}</p>
						<p>Titolo originale: {{ movie.original_title }}</p>
						<div>
							Linuga:
							<span v-if="!flags.includes(movie.original_language)">{{
								movie.original_language
							}}</span>
							<div v-else class="d-inline-block flag-img">
								<img :src="getFlagImg(movie.original_language)" alt="" />
							</div>
						</div>

						<p>
							Voto: <i v-for="index in formatNumber(movie.vote_average)" class="fa-solid fa-star"></i>
							<i v-for="index in 5 - formatNumber(movie.vote_average)" class="fa-regular fa-star"></i>
						</p>
					</div>
				</div>
			</div>
		</div>
		<h1 class="text-center">Tv series</h1>
		<div class="d-flex flex-wrap">
			<div class="my-card m-5" v-for="tvSerie in store.series">
				<div class="flip-card-inner">
					<div class="front-card">
						<img v-if="tvSerie.poster_path !== null" :src="URLImage + tvSerie.poster_path" alt="" />
						<img v-else class="placeholder-img" :src="getPlaceholderImg()" alt="" />
					</div>
					<div class="back-card p-5">
						<p>Titolo: {{ tvSerie.name }}</p>
						<p>Titolo originale: {{ tvSerie.original_name }}</p>

						<div>
							Linuga:
							<span v-if="!flags.includes(tvSerie.original_language)">{{
								tvSerie.original_language
							}}</span>
							<div v-else class="d-inline-block flag-img">
								<img :src="getFlagImg(tvSerie.original_language)" alt="" />
							</div>
						</div>
						<p>
							Voto:
							<i v-for="index in formatNumber(tvSerie.vote_average)" class="fa-solid fa-star"></i>
							<i
								v-for="index in 5 - formatNumber(tvSerie.vote_average)"
								class="fa-regular fa-star"
							></i>
						</p>
					</div>
				</div>
			</div>
		</div>
	</main>
</template>

<script>
import { store } from "../store";
export default {
	data() {
		return {
			store,
			flags: ["de", "en", "es", "fr", "it", "ja", "nl", "pl"],
			URLImage: "https://image.tmdb.org/t/p/w342/",
		};
	},
	methods: {
		getFlagImg(lang) {
			return new URL(`../assets/img/${lang}.png`, import.meta.url).href;
		},
		formatNumber(num) {
			return Math.round(num / 2);
		},
		getPlaceholderImg() {
			return new URL(`../assets/img/placeholder.png`, import.meta.url).href;
		},
	},
};
</script>

<style lang="scss" scoped>
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
