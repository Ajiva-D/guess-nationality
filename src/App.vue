<template>
	<div id="app">
		<Header />
		<main>
			<h2>Guess your users Nationality</h2>
			<DataTable :tableValues="tableValues"/>
		</main>
	</div>
</template>

<script>
import Header from "./components/Header";
import DataTable from './components/DataTable'
import UserData from '../data.json'
export default {
	name: "App",
	components: {
		Header,
		DataTable
	},
	data() {
		return {
			tableValues: {
					title:['ID','NAME','EMAIL','GENDER',''],
					keys:['name','email','gender'],
					data:[]
				}
		}
	},
	methods: {
		// async getUsers() {
		// 	let url = '../data.json';
		// 	let res = await fetch(url);
		// 	console.log(res);
		// }
	},
mounted () {
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
main{
	padding:4rem;
	h2{
		font-size:2rem;
		margin-bottom:20px;
	}
}
</style>
