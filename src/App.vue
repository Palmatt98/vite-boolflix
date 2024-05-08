<template>
	<div>
		<SearchBar @eseguiRicerca="callbackEseguiRicerca" />
		<Main :movies="movieArray" :tvSeries="tvArray" />
	</div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
import Main from "./components/Main.vue"
import { store } from "./store.js"
export default {
	components: {
		SearchBar,
    Main,

	},
  data() {
    return {
      baseURL: "https://api.themoviedb.org/3/search",
      store,
      movieArray: [],
      tvArray: [],
    }
  },
  methods: {
    callbackEseguiRicerca(searchText) {
      axios.get(this.baseURL + `/movie?api_key=${store.apiKey}&query=${searchText}`)
        .then((response) => {
          this.movieArray = response.data.results
        })
      axios.get(this.baseURL + `/tv?api_key=${store.apiKey}&query=${searchText}`)
        .then((response) => {
          this.tvArray = response.data.results
        })
    }
  }
};
</script>

<style lang="scss" scoped></style>
