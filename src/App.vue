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
export default {
	name: "App",
	components: {
		Header,
		DataTable
	},
	data() {
		return {
			tableValues: {
					title:['TRANSACTION ID','TYPE','COST','RATE','DATE',''],
					keys:['id','type','cost','rate','date'],
					data:[{
						id:'00TX29283931',
						type:'Amazon',
						cost:'$299',
						rate:'₦150,000',
						date:'11-12-2020'
					},
					{
						id:'79TX99012500',
						type:'Apple',
						cost:'$150',
						rate:'₦50,000',
						date:'13-04-2021'
					}]
				}
		}
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
