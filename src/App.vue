<template>
	<div id="app">
		<Header />
		<main>
			<h2>Guess your users Nationality</h2>
			<DataTable :tableValues="tableValues" @guessCountry="guessCountry($event)" />
		</main>
	</div>
</template>

<script>
import Header from "./components/Header";
import DataTable from "./components/DataTable";
import UserData from "../data.json";
import { mapMutations } from 'vuex';

export default {
	name: "App",
	components: {
		Header,
		DataTable,
	},
	data() {
		return {
			tableValues:{
				titles: ["ID", "NAME", "EMAIL", "GENDER", "COUNTRY"],
				keys: ["name", "email", "gender"],
				data: [],
			}
		};
	},
	methods: {
		async guessCountry(user) {
			this.updateIsGuessing({id:user.index, status:true});
			let url = `https://api.nationalize.io?name=${user.name}`;
			let res = await fetch(url);
			let data = await res.json();
			let regionNames = new Intl.DisplayNames(["en"], { type: "region" });
			let country = data.country[0] ? regionNames.of(data.country[0].country_id) : 'None';
			this.$set(this.tableValues.data[user.userID-1], 'country', country);
			this.updateIsGuessing({id:user.index, status:false});
		},
		...mapMutations([
			'updateIsGuessing', //also supports payload `this.nameOfMutation(amount)` 
		])
	},
	mounted() {
		this.tableValues.data = UserData;
	},
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400&display=swap");
#app {
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}
body,
* {
	font-family: "Inter", sans-serif;
	margin: 0;
}
main {
	padding: 4rem;
	h2 {
		font-size: 2rem;
		margin-bottom: 20px;
	}
}
/* @media screen and (min-width:768px) and (max-width:999px){
	main{
		padding:
	}
} */
@media screen and (max-width:999px){
main{
	padding:4rem 2rem;
}
}
</style>
