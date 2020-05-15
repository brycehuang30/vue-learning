/* eslint-disable no-undef */
<template>
    <div class="buttons-wrapper">
        <Screen :value="screen" />
        <div class="number-buttons">
            <NumberButton
                v-for="(n,index) in number"
                :key="index"
                :number="n"
                @click.native="digit(n)"
            />
            <NumberButton
                :number="0"
                @click.native="digit(0)"
            />
        </div>
        <div class="buttons-row">
            <ResetButton
                @click.native="reset"
            />
            <SumButton
                @click.native="op(add)"
            />
            <MulButton
                @click.native="op(mul)"
            />
            <EqualButton
                @click.native="equel"
            />
        </div>
        <div>
            caculator現在狀態： {{ caculator }}
        </div>
    </div>
</template>

<script>
// @ is an alias to /src
import Screen from "@/components/Screen.vue";
import NumberButton from "@/components/NumberButton.vue";
import ResetButton from "@/components/ResetButton.vue";
import SumButton from "@/components/SumButton.vue";
import MulButton from "@/components/MulButton.vue";
import EqualButton from "@/components/EqualButton.vue";


export default {
    name: "Buttons",
    components: {
        Screen,
        NumberButton,
        ResetButton,
        SumButton,
        MulButton,
        EqualButton,
    },
    data() {
        return {

            number: [1, 2, 3, 4, 5, 6, 7, 8, 9],

            leftValue: 0,
            rightValue: 0,
            screen: 0,

            currentStatus: 0,
            INPUT_LEFT_STATE: 0,
            INPUT_RIGHT_STATE: 1,
            SHOW_ANSWER_STATE: 2,
            ERROR_STATE: 3,

            // 這個變數裡面存的是一個「函數」
            operation: Function,
        };
    },
    computed: {
        caculator() {
            // 根據目前的狀態顯示文字
            switch (this.currentStatus) {
                case this.INPUT_LEFT_STATE:
                    return `全新的左半${this.leftValue}`;

                case this.INPUT_RIGHT_STATE:
                    return `按了加號的右半${this.rightValue}`;

                case this.SHOW_ANSWER_STATE:
                    return `按了等於合計是${this.operation(this.leftValue, this.rightValue)}`;

                case this.ERROR_STATE:
                    return "錯誤";

                default:
                    return "Error";
            }
        },
    },
    methods: {
        digit(value) {
            switch (this.currentStatus) {
                case this.INPUT_LEFT_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    this.leftValue = this.leftValue * 10 + value;
                    this.screen = this.leftValue;
                    break;

                case this.INPUT_RIGHT_STATE:
                    this.currentStatus = this.INPUT_RIGHT_STATE;
                    this.rightValue = this.rightValue * 10 + value;
                    this.screen = this.rightValue;
                    break;

                case this.SHOW_ANSWER_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    this.leftValue = value;
                    this.rightValue = 0;
                    this.screen = value;
                    break;

                case this.ERROR_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    this.leftValue = value;
                    this.rightValue = 0;
                    this.screen = value;
                    break;

                default:
                    console.log(`unexpected state${this.currentStatus}`);
            }
        },
        op(operation) {
            // 更新運算符號
            this.operation = operation;
            switch (this.currentStatus) {
                case this.INPUT_LEFT_STATE:
                    this.currentStatus = this.INPUT_RIGHT_STATE;
                    break;

                case this.INPUT_RIGHT_STATE:
                    this.currentStatus = this.INPUT_RIGHT_STATE;
                    this.leftValue += this.screen;
                    this.rightValue = 0;
                    this.screen = this.leftValue;
                    break;

                case this.SHOW_ANSWER_STATE:
                    this.currentStatus = this.INPUT_RIGHT_STATE;
                    this.leftValue = this.screen;
                    this.rightValue = 0;
                    break;

                case this.ERROR_STATE:
                    this.currentStatus = this.INPUT_RIGHT_STATE;
                    this.leftValue = this.screen;
                    this.rightValue = 0;
                    break;

                default:
                    console.log(`unexpected state${this.currentStatus}`);
            }
        },
        equel() {
            switch (this.currentStatus) {
                case this.INPUT_LEFT_STATE:
                    this.currentStatus = this.ERROR_STATE;
                    break;

                case this.INPUT_RIGHT_STATE:
                    this.currentStatus = this.SHOW_ANSWER_STATE;
                    // 把要運算的數值 left 跟 right 丟到稍早設定的運算符號(運算function)去執行
                    this.screen = this.operation(this.leftValue, this.rightValue);
                    break;

                case this.SHOW_ANSWER_STATE:
                    this.currentStatus = this.ERROR_STATE;
                    break;

                case this.ERROR_STATE:
                    this.currentStatus = this.ERROR_STATE;
                    break;

                default:
                    console.log(`unexpected state${this.currentStatus}`);
            }
        },
        reset() {
            switch (this.currentStatus) {
                case this.INPUT_LEFT_STATE:
                case this.INPUT_RIGHT_STATE:
                case this.SHOW_ANSWER_STATE:
                case this.ERROR_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    this.leftValue = 0;
                    this.rightValue = 0;
                    this.screen = 0;
                    break;
                default:
                    console.log(`unexpected state${this.currentStatus}`);
            }
        },
        add(a, b) {
            return a + b;
        },
        mul(a, b) {
            return a * b;
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
    .number-buttons{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        width: 180px;
        background-color: #ff837f;
        padding: 3px;
    }
    .buttons-row {
        display: flex;
        flex-direction: row;
        justify-content: center;
    }
}
</style>
