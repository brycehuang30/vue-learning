<template>
    <div class="buttons">
        <ClickCountButton
            v-for="index in clickCountButtonNum"
            :key="index"
        />
        <ResetButton />
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
    },
};
</script>

<style lang="scss" scoped>
.buttons {
    display: flex;
    flex-direction: row;
    justify-content: center;
}
</style>
