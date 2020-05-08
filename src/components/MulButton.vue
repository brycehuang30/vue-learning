<template>
    <div
        class="mul-button"
        @click="sendMulSignal"
    >
        Mul
    </div>
</template>

<script lang="ts">

import Vue from "vue";

export default Vue.extend({
    name: "MulButton",
    props: {
    },
    data() {
        return {
        };
    },
    methods: {
        sendMulSignal() {
            this.$root.$emit("mul-buttons");
        },
    },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.mul-button {
    width: 50px;
    height: 30px;
    background-color: #2a5019;
    color: white;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 10px;
    margin: 3px;
}
</style>
