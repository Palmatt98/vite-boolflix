<template>
	<main>
		<div class="d-flex flex-wrap">
			<div class="my-card m-2 p-2" v-for="movie in movies">
				<p>Titolo: {{ movie.title }}</p>
				<p>Titolo originale: {{ movie.original_title }}</p>
				<p>Linuga: {{ movie.original_language }}</p>
				<p>Voto: {{ movie.vote_average }}</p>
			</div>
		</div>
	</main>
</template>

<script>
export default {
	props: {
		movies: Array,
	},
};
</script>

<style lang="scss" scoped>
.my-card {
	border: 1px solid black;
	border-radius: 5px;

}
</style>
