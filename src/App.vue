<template>
	<div>
		<header class="px-4">
			<div class="logo">
				<h1>BOOLFLIX</h1>
			</div>
			<SearchBar @eseguiRicerca="callbackEseguiRicerca" />
		</header>
		<Main />
	</div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
import Main from "./components/Main.vue";
import { store } from "./store.js";
export default {
	components: {
		SearchBar,
		Main,
		
	},
	data() {
		return {
			baseURL: "https://api.themoviedb.org/3/search",
			store,
		};
	},
	methods: {
		callbackEseguiRicerca() {
			axios
				.get(this.baseURL + `/movie?api_key=${store.apiKey}&query=${store.searchText}`)
				.then((response) => {
					store.movies = response.data.results;
				});
			axios
				.get(this.baseURL + `/tv?api_key=${store.apiKey}&query=${store.searchText}`)
				.then((response) => {
					store.series = response.data.results;
				});
		},
	},
};
</script>

<style lang="scss" scoped>
header {
	height: 80px;
	background-color: black;
	display: flex;
	justify-content: space-between;
	align-items: center;
	.logo {
		color: red;
	}
}
</style>
