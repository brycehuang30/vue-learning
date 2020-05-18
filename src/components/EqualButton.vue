<template>
    <div
        class="equal-button"
        @click="sendMulSignal"
    >
        <h1>=</h1>
    </div>
</template>

<script lang="ts">

import Vue from "vue";

export default Vue.extend({
    name: "EqualButton",
    props: {
    },
    data() {
        return {
        };
    },
    methods: {
        sendMulSignal() {
            this.$root.$emit("equal-buttons");
        },
    },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.equal-button {
    width: 50px;
    height: 50px;
    background-color: #f29604;
    color: #ffffff;
    border-radius: 50%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 10px;
    margin: 3px;
}
.equal-button:hover{
    cursor: pointer;
    background-color: #ffffff;
    color: #f29604;
}
</style>
