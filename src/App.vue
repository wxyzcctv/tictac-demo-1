<template>
	<div>
		<div class="wrapper">
			<div>第{{n}}手</div>
			<div class="row">
				<Cell @click="onClickCell(0,$event)" :n="n" />
				<Cell v-on:click="onClickCell(1,$event)" v-bind:n="n" :end="end" />
				<Cell v-on:click="onClickCell(2,$event)" v-bind:n="n" :end="end" />
			</div>
			<div class="row">
				<Cell v-on:click="onClickCell(3,$event)" v-bind:n="n" :end="end" />
				<Cell v-on:click="onClickCell(4,$event)" v-bind:n="n" :end="end" />
				<Cell v-on:click="onClickCell(5,$event)" v-bind:n="n" :end="end" />
			</div>
			<div class="row">
				<Cell v-on:click="onClickCell(6,$event)" v-bind:n="n" :end="end" />
				<Cell v-on:click="onClickCell(7,$event)" v-bind:n="n" :end="end" />
				<Cell v-on:click="onClickCell(8,$event)" v-bind:n="n" :end="end" />
			</div>
			<div>对弈结果：{{result === null ? '未分胜负' : result + '胜出'}}</div>
		</div>
	</div>
</template>

<script>
import Cell from "./components/Cell.vue";

export default {
	components: {
		Cell,
	},
	data() {
		return {
			n: 0,
			map: [
				[null, null, null],
				[null, null, null],
				[null, null, null],
			],
			result: null,
			end: "",
		};
	},
	methods: {
		onClickCell(i, text) {
			this.map[Math.floor(i / 3)][i % 3] = text;
			this.n += 1;
			this.tell();
		},
		tell() {
			const map = this.map;
			for (let i = 0; i < map.length; i++) {
				if (
					map[i][0] !== null &&
					map[i][0] === map[i][1] &&
					map[i][1] === map[i][2]
				) {
					this.result = map[i][0];
				}
			}
			for (let j = 0; j < map.length; j++) {
				if (
					map[0][j] !== null &&
					map[0][j] === map[1][j] &&
					map[1][j] === map[2][j]
				) {
					this.result = map[0][j];
				}
			}
			if (
				map[0][0] !== null &&
				map[0][0] === map[1][1] &&
				map[1][1] === map[2][2]
			) {
				this.result = map[0][0];
			}
			if (
				map[0][2] !== null &&
				map[0][2] === map[1][1] &&
				map[1][1] === map[2][0]
			) {
				this.result = map[0][2];
			}
			if(this.result){
				this.end = "finish"
			}
		},
	},
};
</script>

<style>
.wrapper {
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
}
.row {
	display: flex;
}
</style>
