<template>
    <div class="buttons">
        <div class="row-wrapper">
            <ClickCountButton
                v-for="index in clickCountButtonNum"
                :key="index"
            />
        </div>
        <div class="row-wrapper">
            <div
                class="operation-button"
                @click="plusButtonCount"
            >
                +
            </div>
            <div
                class="operation-button"
                @click="minusButtonCount"
            >
                -
            </div>
        </div>
    </div>
</template>

<script>
// @ is an alias to /src
import ClickCountButton from "@/components/ClickCountButton.vue";

export default {
    name: "Buttons",
    components: {
        ClickCountButton,
    },
    data() {
        return {
            clickCountButtonNum: 5,
        };
    },
    methods: {
        plusButtonCount() {
            this.clickCountButtonNum += 1;
        },
        minusButtonCount() {
            if (this.clickCountButtonNum > 0) {
                this.clickCountButtonNum -= 1;
            }
        },
    },
};
</script>

<style lang="scss" scoped>
.buttons {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .row-wrapper {
        height: 5vw;
        display: flex;
        flex-direction: row;
        justify-content: center;
    }


    .operation-button {
        width: 50px;
        height: 30px;
        background-color: rgb(140, 127, 255);
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
