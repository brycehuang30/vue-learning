<template>
    <div
        class="click-count-button"
        @click="addOne"
    >
        {{ clickCount }}
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
.click-count-button {
    width: 50px;
    height: 30px;
    background-color: aquamarine;
    color: black;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 10px;
    margin: 3px;
}
</style>
