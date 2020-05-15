/* eslint-disable no-undef */
<template>
    <div class="buttons-wrapper">
        <Screen :value="answer" />
        <div class="number-buttons">
            <NumberButton
                v-for="(n,index) in number"
                :key="index"
                :number="n"
                @click.native="add(n)"
            />
            <NumberButton
                :number="0"
                @click.native="add(0)"
            />
        </div>
        <div class="buttons-row">
            <ResetButton />
            <SumButton />
            <MulButton />
            <EqualButton />
        </div>
        <div>
            numberstring1: {{ numberstring1 }}
        </div>
        <div>
            numberstring2: {{ numberstring2 }}
        </div>
        <div>
            caculator現在狀態： {{ caculator }}
        </div>
        <div>
            <NumberButton
                @click.native="digit"
            />
            <SumButton
                @click.native="op"
            />
            <MulButton
                @click.native="op"
            />
            <NumberButton
                @click.native="digit"
            />
            <EqualButton
                @click.native="equel"
            />
            <ResetButton
                @click.native="reset"
            />
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
            answer: 0,
            number: [1, 2, 3, 4, 5, 6, 7, 8, 9],
            numberstring1: 0,
            numberstring2: 0,

            currentStatus: 0,
            INPUT_LEFT_STATE: 0,
            INPUT_RIGHT_STATE: 1,
            SHOW_ANSWER_STATE: 2,
            ERROR_STATE: 3,
        };
    },
    computed: {
        caculator() {
            // 根據目前的狀態顯示文字
            switch (this.currentStatus) {
                case this.INPUT_LEFT_STATE:
                    return "輸入左半數字";

                case this.INPUT_RIGHT_STATE:
                    return "輸入右半數字";

                case this.SHOW_ANSWER_STATE:
                    return "顯示答案";

                case this.ERROR_STATE:
                    return "錯誤";

                default:
                    return "Error";
            }
        },
    },
    mounted() {
        this.$root.$on("reset-buttons", () => {
            this.clear();
        });
        this.$root.$on("sum-buttons", () => {
            this.sum();
            this.screenzero();
            this.store();
        });
        this.$root.$on("mul-buttons", () => {
            if (this.numberstring2 === 0) {
                this.numberstring2 = this.numberstring1;
                this.numberstring1 = 1;
                this.mul();
                this.store();
                this.screenzero();
            } else {
                this.mul();
                this.store();
                this.screenzero();
            }
        });

        // this.$root.$on("equal-buttons", () => {
        // });
    },
    methods: {
        add(value) {
            if (this.answer === 0) {
                this.numberstring1 = String(value);
                this.answer = this.numberstring1;
            } else {
                this.numberstring1 += String(value);
                this.answer = this.numberstring1;
            }
        },
        clear() {
            this.answer = 0;
            this.numberstring1 = 0;
            this.numberstring2 = 0;
        },
        store() {
            this.numberstring2 = this.answer;
        },
        sum() {
            this.answer = parseInt(this.numberstring1, 10) + parseInt(this.numberstring2, 10);
        },
        mul() {
            this.answer = parseInt(this.numberstring1, 10) * parseInt(this.numberstring2, 10);
        },
        screenzero() {
            this.numberstring1 = 0;
        },
        digit() {
            switch (this.currentStatus) {
                case this.INPUT_LEFT_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    break;

                case this.INPUT_RIGHT_STATE:
                    this.currentStatus = this.INPUT_RIGHT_STATE;
                    break;

                case this.SHOW_ANSWER_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    break;

                case this.ERROR_STATE:
                    this.currentStatus = this.ERROR_STATE;
                    break;

                default:
                    console.log(`unexpected state${this.currentStatus}`);
            }
        },
        op() {
            switch (this.currentStatus) {
                case this.INPUT_LEFT_STATE:
                    this.currentStatus = this.INPUT_RIGHT_STATE;
                    break;

                case this.INPUT_RIGHT_STATE:
                    this.currentStatus = this.ERROR_STATE;
                    break;

                case this.SHOW_ANSWER_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    break;

                case this.ERROR_STATE:
                    this.currentStatus = this.ERROR_STATE;
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
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    break;

                case this.INPUT_RIGHT_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    break;

                case this.SHOW_ANSWER_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    break;

                case this.ERROR_STATE:
                    this.currentStatus = this.INPUT_LEFT_STATE;
                    break;

                default:
                    console.log(`unexpected state${this.currentStatus}`);
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
