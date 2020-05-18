<template>
    <div
        class="reset-button"
        @click="sendResetSignal"
    >
        <h1>AC</h1>
    </div>
</template>

<script lang="ts">

import Vue from "vue";

export default Vue.extend({
    name: "ResetButton",
    props: {
    },
    data() {
        return {
        };
    },
    methods: {
        sendResetSignal() {
            this.$root.$emit("reset-buttons");
        },
    },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.reset-button {
    width: 50px;
    height: 50px;
    background-color: #a5a5a5;
    color: #000;
    border-radius: 50%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 10px;
    margin: 3px;
}
.reset-button:hover{
    cursor: pointer;
    background-color: #ffffff;
    color: #000;
}
</style>
