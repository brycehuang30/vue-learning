<template>
    <div class="buttons-wrapper">
        <Screen :value="buttonSum" />
        <div class="buttons-row">
            <ClickCountButton
                v-for="index in clickCountButtonNum"
                :key="index"
                @submit-value="addToSum"
                @mul-value="mul"
            />
        </div>
        <div class="buttons-row">
            <NumberButton />
        </div>
        <div class="buttons-row">
            <ResetButton />
            <SumButton />
            <MulButton />
        </div>
    </div>
</template>

<script>
// @ is an alias to /src
import ClickCountButton from "@/components/ClickCountButton.vue";
import ResetButton from "@/components/ResetButton.vue";
import SumButton from "@/components/SumButton.vue";
import Screen from "@/components/Screen.vue";
import MulButton from "@/components/MulButton.vue";
import NumberButton from "@/components/NumberButton.vue";


export default {
    name: "Buttons",
    components: {
        ClickCountButton,
        ResetButton,
        SumButton,
        Screen,
        MulButton,
        NumberButton,
    },
    data() {
        return {
            clickCountButtonNum: 5,
            buttonSum: 0,
        };
    },
    mounted() {
        this.$root.$on("reset-buttons", () => {
            this.buttonSum = 0;
        });
    },
    methods: {
        addToSum(value) {
            this.buttonSum += value;
        },
        mul(value) {
            if (this.buttonSum === 0) {
                this.buttonSum = value;
            } else {
                this.buttonSum *= value;
            }
        },
    },
};
</script>

<style lang="scss" scoped>
.buttons-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .buttons-row {
        display: flex;
        flex-direction: row;
        justify-content: center;
    }
}
</style>
