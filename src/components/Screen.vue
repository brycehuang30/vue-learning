<template>
    <div
        class="screen"
    >
        {{ value }}
    </div>
</template>

<script lang="ts">

import Vue from "vue";

export default Vue.extend({
    name: "Screen",
    props: {
        value: {
            type: Number,
            required: false,
            default: 0,
        },
    },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.screen {
    width: 100%;
    height: 40px;
    box-sizing: border-box;
    background-color: #000;
    color: #fff;
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;
    font-size: 50px;
    margin: 20px 0;
    padding: 20px 30px;
}
</style>
