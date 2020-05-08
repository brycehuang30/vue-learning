<template>
    <div
        class="sum-button"
        @click="sendSumSignal"
    >
        Sum
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
    height: 30px;
    background-color: rgb(25, 46, 80);
    color: white;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 10px;
    margin: 3px;
}
</style>
