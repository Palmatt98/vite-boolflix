<template>
	<div>
		<div class="input-group my-3 w-50 mx-auto">
			<input v-model="store.searchText" type="text" class="form-control" placeholder="Cerca film o serie TV" />
			<button @click="searchMovie" class="btn btn-outline-primary" type="button">
				<i class="fa-solid fa-magnifying-glass"></i>
			</button>
		</div>
	</div>
</template>

<script>
import { store } from '../store';
export default {
	data() {
		return{
			store,
		}
	},
	methods: {
		searchMovie(){
			if(store.searchText === ""){
				return
			}
			this.$emit("eseguiRicerca",);
		}
	}
};
</script>

<style lang="scss" scoped></style>
