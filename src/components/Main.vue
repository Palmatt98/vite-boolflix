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
				<p>Voto: {{ movie.vote_average }}</p>
			</div>
		</div>
		<h1 class="text-center">Tv series</h1>
		<div class="d-flex flex-wrap">
			<div class="my-card m-2 p-2" v-for="tvSerie in tvSeries">
				<p>Titolo: {{ tvSerie.name }}</p>
				<p>Titolo originale: {{ tvSerie.original_name }}</p>
				<div>
					Linuga:
					<span v-if="!flags.includes(tvSerie.original_language)">{{ tvSerie.original_language }}</span>
					<div v-else class="d-inline-block flag-img">
						<img :src="getFlagImg(tvSerie.original_language)" alt="" />
					</div>
				</div>
				<p>Voto: {{ tvSerie.vote_average }}</p>
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
		};
	},
	methods: {
		getFlagImg(lang) {
			return new URL(`../assets/img/${lang}.png`, import.meta.url).href;
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
