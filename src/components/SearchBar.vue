<template>
	<div>
		<div class="input-group my-3 w-50 mx-auto">
			<input v-model="searchText" type="text" class="form-control" placeholder="Cerca film o serie TV" />
			<button @click="searchMovie" class="btn btn-outline-primary" type="button">
				<i class="fa-solid fa-magnifying-glass"></i>
			</button>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return{
			searchText: "",
		}
	},
	methods: {
		searchMovie(){
			if(this.searchText === ""){
				return
			}
			this.$emit("eseguiRicerca", this.searchText);
		}
	}
};
</script>

<style lang="scss" scoped></style>
