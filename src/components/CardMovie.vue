<template>
	<div class="my-card m-5" >
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
					<span v-if="!flags.includes(movie.original_language)">{{ movie.original_language }}</span>
					<div v-else class="d-inline-block flag-img">
						<img :src="getFlagImg(movie.original_language)" alt="" />
					</div>
				</div>

				<p>
					Voto: <i v-for="index in formatNumber(movie.vote_average)" class="fa-solid fa-star"></i>
					<i v-for="index in 5 - formatNumber(movie.vote_average)" class="fa-regular fa-star"></i>
				</p>
				<ul>
					<p>Cast:</p>
					<li v-for="item in cast">
						{{ item !== undefined ? item.name : null }}
					</li>
					<p>Generi:</p>
					<li v-for="item in genres">
						{{ item !== undefined ? item.name : null }}
					</li>
					
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		movie: Object,
		cast: Array,
		genres: Array,
	},
	data(){
		return {
			flags: ["de", "en", "es", "fr", "it", "ja", "nl", "pl"],
			URLImage: "https://image.tmdb.org/t/p/w342/",
		}
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
	}
};
</script>

<style lang="scss" scoped></style>
