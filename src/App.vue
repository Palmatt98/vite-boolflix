<template>
	<div>
		<SearchBar @eseguiRicerca="callbackEseguiRicerca" />
		<Main :movies="movieArray" />
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
      baseURLMovie: "https://api.themoviedb.org/3/search/movie",
      store,
      movieArray: [],
    }
  },
  methods: {
    callbackEseguiRicerca(searchText) {
      axios.get(this.baseURLMovie + `?api_key=${store.apiKey}&query=${searchText}`)
        .then((response) => {
          this.movieArray = response.data.results
        })
    }
  }
};
</script>

<style lang="scss" scoped></style>
