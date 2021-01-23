<template>
		<table>
			<thead>
				<tr>
					<th v-for="(title, index) in tableValues.title" :key="index">
						{{ title }}
					</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="item in tableValues.data" :key="item.id">
					<td v-for="arrayKey in tableValues.keys" :key="arrayKey">
						{{ item[arrayKey] }}
					</td>
					<td>
						<button>Guess Country</button>
					</td>
				</tr>
			</tbody>
		</table>
</template>

<script>
export default {
	props: {
		tableValues: {
			type: Object,
			default: function () {
        return {}
      },
		},
	},
};
</script>

<style lang="scss" scoped>
table{
	border:1px solid #EDEDED;
	width:100%;
	border-collapse: collapse;
	tr, th, td{
			border:1px solid #EDEDED;
			padding:10px;
	}
	th{
		background: #038695;
		color:#fff;
		text-align: left;
	}
	button{
		background-color: #fc6435;
		border-radius: 12px;
		color:#fff;
		padding:10px 20px;
		border:none;
	}
}
</style>
