<template>
	<main>
		<h1 class="text-center">Movies</h1>
		<div class="d-flex flex-wrap">
			<div class="my-card m-2 p-2" v-for="movie in movies">
				<p>Titolo: {{ movie.title }}</p>
				<p>Titolo originale: {{ movie.original_title }}</p>
				<div>
					Linuga:
					<span v-if="!flags.includes(movie.original_language)">{{ movie.original_language }}</span>
					<div v-else class="d-inline-block flag-img">
						<img :src="getFlagImg(movie.original_language)" alt="" />
					</div>
				</div>

				<p>
					Voto: <i v-for="index in formatNumber(movie.vote_average)" class="fa-solid fa-star"></i>
					<i v-for="index in 5 - formatNumber(movie.vote_average)" class="fa-regular fa-star"></i>
				</p>
				<img :src="URLImage + movie.poster_path" alt="" />
			</div>
		</div>
		<h1 class="text-center">Tv series</h1>
		<div class="d-flex flex-wrap">
			<div class="my-card m-2 p-2" v-for="tvSerie in tvSeries">
				<p>Titolo: {{ tvSerie.name }}</p>
				<p>Titolo originale: {{ tvSerie.original_name }}</p>
				<img :src="URLImage + tvSerie.poster_path" alt="" />
				<div>
					Linuga:
					<span v-if="!flags.includes(tvSerie.original_language)">{{ tvSerie.original_language }}</span>
					<div v-else class="d-inline-block flag-img">
						<img :src="getFlagImg(tvSerie.original_language)" alt="" />
					</div>
				</div>
				<p>
					Voto:
					<i v-for="index in formatNumber(tvSerie.vote_average)" class="fa-solid fa-star"></i>
					<i v-for="index in 5 - formatNumber(tvSerie.vote_average)" class="fa-regular fa-star"></i>
					<!-- {{ formatNumber(tvSerie.vote_average) }} -->
				</p>
			</div>
		</div>
	</main>
</template>

<script>
export default {
	props: {
		movies: Array,
		tvSeries: Array,
	},
	data() {
		return {
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
	},
};
</script>

<style lang="scss" scoped>
.my-card {
	border: 1px solid black;
	border-radius: 5px;
	.flag-img {
		width: 25px;
		img {
			width: 100%;
		}
	}
}
</style>
