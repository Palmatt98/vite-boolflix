<template>
	<div class="my-card m-5">
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
					<span v-if="!flags.includes(tvSerie.original_language)">{{ tvSerie.original_language }}</span>
					<div v-else class="d-inline-block flag-img">
						<img :src="getFlagImg(tvSerie.original_language)" alt="" />
					</div>
				</div>
				<p>
					Voto:
					<i v-for="index in formatNumber(tvSerie.vote_average)" class="fa-solid fa-star"></i>
					<i v-for="index in 5 - formatNumber(tvSerie.vote_average)" class="fa-regular fa-star"></i>
				</p>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		tvSerie: Object,
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
		getPlaceholderImg() {
			return new URL(`../assets/img/placeholder.png`, import.meta.url).href;
		},
	},
};
</script>

<style lang="scss" scoped></style>
