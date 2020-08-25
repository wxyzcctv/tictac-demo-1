<template>
    <div class="cell" v-on:click="a = true">
        <template v-if="a">{{text}}</template>
        <template v-else></template>
    </div>
</template>

<script>
export default {
    data(){
        return{ a: false, text: "O"}
    }
}
</script>

<style>
    .cell{
        border: 1px solid black;
        height: 100px;
        width: 100px;
        font-size: 80px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>

