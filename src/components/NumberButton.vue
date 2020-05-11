<template>
    <div>
        <div class="button">
            <div
                class="number-button"
                @click="add"
            >
                {{ aa }}
            </div>
            <div
                class="number-button"
                @click="add"
            >
                2
            </div>
            <div
                class="number-button"
                @click="add"
            >
                3
            </div>
            <div
                class="number-button"
                @click="add"
            >
                4
            </div>
            <div
                class="number-button"
                @click="add"
            >
                5
            </div>
            <div
                class="number-button"
                @click="add"
            >
                6
            </div>
            <div
                class="number-button"
                @click="add"
            >
                7
            </div>
            <div
                class="number-button"
                @click="add"
            >
                8
            </div>
            <div
                class="number-button"
                @click="add"
            >
                9
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
    name: "ClickCountButton",
    props: {
        msg: {
            type: String,
            default: "",
            required: false,
        },
    },
    data() {
        return {
            clickCount: 0,
            aa: 100,
        };
    },
    mounted() {
        this.$root.$on("reset-buttons", () => {
            this.clickCount = 0;
        });

        this.$root.$on("sum-buttons", () => {
            this.$emit("submit-value", this.clickCount);
            this.clickCount = 0;
        });
        this.$root.$on("mul-buttons", () => {
            if (this.clickCount > 0) {
                this.$emit("mul-value", this.clickCount);
                this.clickCount = 0;
            }
        });
    },
    methods: {
        addOne() {
            this.clickCount += 1;
        },
    },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.button{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    width: 180px;
    background-color: #ff837f;
    padding: 3px;
    .number-button {
        width: 50px;
        height: 30px;
        background-color: #fff27f;
        color: black;
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        font-size: 10px;
        margin: 3px;
    }
}
</style>
