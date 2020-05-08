<template>
    <div
        class="reset-button"
        @click="sendResetSignal"
    >
        Reset
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
    height: 30px;
    background-color: red;
    color: black;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 10px;
    margin: 3px;
}
</style>
