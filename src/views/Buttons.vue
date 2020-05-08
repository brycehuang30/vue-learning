<template>
    <div class="buttons-wrapper">
        <Screen :value="buttonSum" />
        <div class="buttons-row">
            <ClickCountButton
                v-for="index in clickCountButtonNum"
                :key="index"
            />
        </div>
        <div class="buttons-row">
            <ResetButton />
        </div>
    </div>
</template>

<script>
// @ is an alias to /src
import ClickCountButton from "@/components/ClickCountButton.vue";
import ResetButton from "@/components/ResetButton.vue";
import Screen from "@/components/Screen.vue";

export default {
    name: "Buttons",
    components: {
        ClickCountButton,
        ResetButton,
        Screen,
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
