<template>
	<div>
		<div class="cell" v-on:click="onClickSelf">
			<template v-if="a">{{text}}</template>
		</div>
	</div>
</template>

<script>
export default {
	props: ["n","end"],
	data() {
		return { a: false, text: "" };
	},
	methods: {
		onClickSelf() {
			if (this.text !== "") {
				return;
			}
			if (this.end === "finish") {
				this.a = false;
			} else {
				this.a = true;
				this.text = this.n % 2 !== 0 ? "X" : "O";
				this.$emit("click", this.text);
			}
		},
	},
};
</script>

<style>
.cell {
	border: 1px solid black;
	height: 100px;
	width: 100px;
	font-size: 80px;
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>

