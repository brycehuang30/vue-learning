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
    width: 300px;
    height: 40px;
    background-color: rgb(166,166,149);
    color: rgb(40,40,40);
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;
    font-size: 40px;
    margin: 3px;
    padding: 3px 5px;
}
</style>
