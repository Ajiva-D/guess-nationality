<template>
	<div>
		<table>
			<thead>
				<tr>
					<th v-for="(title, index) in tableValues.title" :key="index">
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
					<td>
						<button>Guess Country</button>
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
	},
};
</script>

<style lang="scss" scoped>
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
