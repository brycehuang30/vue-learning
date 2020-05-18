<template>
    <div
        class="sum-button"
        @click="sendSumSignal"
    >
        <h1>+</h1>
    </div>
</template>

<script lang="ts">

import Vue from "vue";

export default Vue.extend({
    name: "SumButton",
    props: {
    },
    data() {
        return {
        };
    },
    methods: {
        sendSumSignal() {
            this.$root.$emit("sum-buttons");
        },
    },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.sum-button {
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
.sum-button:hover{
    cursor: pointer;
    background-color: #ffffff;
    color: #f29604;
}
</style>
