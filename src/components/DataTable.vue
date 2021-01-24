<template>
	<div class="table-con">
		<table>
			<thead>
				<tr>
					<th v-for="(title, index) in tableValues.titles" :key="index">
						{{ title }}
					</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="(item, i) in pageData" :key="item.id">
					<td>{{ i + 1 }}</td>
					<td v-for="arrayKey in tableValues.keys" :key="arrayKey">
						{{ item[arrayKey] }}
					</td>
					<td v-if="item.country">{{item.country}}</td>
					<td v-else>
						<button @click="$emit('guessCountry',{index:i,userID:item.id, name:item.name})" :disabled="isGuessing.status && isGuessing.id === i">
							<span v-if="isGuessing.status && isGuessing.id === i">Guessing...</span>
							<span v-else>Guess Country</span>
						</button>
					</td>
				</tr>
			</tbody>
		</table>
		<div class="pagination-btns">
			<p>Showing {{ offset + 1 }} to {{ offset + 10 }}</p>
			<div>
				<button class="prev" @click="offset -= 10" :disabled="prevDisabled">Prev</button>
				<button class="next" @click="offset += 10" :disabled="nextDisabled">Next</button>
			</div>
		</div>
	</div>
</template>

<script>
import { mapState } from 'vuex';

export default {
	props: {
		tableValues: {
			type: Object,
			default: function() {
				return {};
			},
		},
	},
	data() {
		return {
			offset: 0,
			prevDisabled:false,
			nextDisabled:false
		};
	},
	computed: {
		pageData() {
			/* eslint-disable-next-line */
			this.prevDisabled = this.offset <= 0 ?  true :  false;
	
			/* eslint-disable-next-line */
			this.nextDisabled = this.offset >= this.tableValues.data.length - 10 ?  true : false;

			let offsetEnd = this.offset + 10;
			return this.tableValues.data.slice(this.offset, offsetEnd);
		},
		...mapState([
			'isGuessing',
		])
	},
};
</script>

<style lang="scss" scoped>
.table-con{
	overflow-x: auto;
}
table {
	border: 1px solid #ededed;
	width: 100%;
	border-collapse: collapse;
	tr,
	th,
	td {
		border: 1px solid #ededed;
		padding: 10px;
	}
	th {
		background: #038695;
		color: #fff;
		text-align: left;
	}
	button {
		background-color: #fc6435;
		border-radius: 12px;
		color: #fff;
		padding: 10px 20px;
		border: none;
		width:200px;
		&:disabled{
		background-color: #e07c5e;
		color:#dbd7d7;
	}
	}
	
}
.pagination-btns {
	margin-top: 30px;
	display: flex;
	justify-content: space-between;
	button {
		background-color: #ffd2c4;
		border: none;
		padding: 5px 15px;
		color: #046f7a;
		font-weight: bold;
	}
	button:disabled {
		color: #7fc0c7;
		background-color: #fcf3f0;
	}
	.prev {
		margin-right: 10px;
		border-radius: 6px 0 0 6px;
	}
	.next {
		border-radius: 0 6px 6px 0;
	}
}
</style>
