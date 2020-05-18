<template>
    <div class="button">
        <div
            :style="{width: width + 'px'}"
            class="number-button"
            @click="add"
        >
            <h1>{{ number }}</h1>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
    name: "NumberButton",
    props: {
        number: {
            type: Number,
            default: 0,
        },
        width: {
            type: Number,
            default: 50,
        },
    },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.number-button {
    width: 50px;
    height: 50px;
    background-color: rgb(49, 49, 49);
    color: #fff;
    border-radius: 50px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 10px;
    margin: 3px;
    h1{
        font-size: 25px;
        padding: 0;
        margin: 0;
        font-weight: 300;
    }
}

.number-button:hover{
    cursor: pointer;
    background-color: #727272;
}

</style>
