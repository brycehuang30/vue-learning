<template>
    <div class="buttons-wrapper">
        <Screen :value="screenValue" />
        <div class="number-buttons">
            <NumberButton
                v-for="(n,index) in number"
                :key="index"
                :number="n"
                @click.native="inputValue(n)"
            />
            <NumberButton
                :number="0"
                @click.native="inputValue(0)"
            />
        </div>
        <div class="buttons-row">
            <ResetButton />
            <SumButton />
            <MulButton />
            <EqualButton />
        </div>
        <div>
            currentInput: {{ currentInput }}
        </div>
        <div>
            answer: {{ answer }}
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
            // screenValue: 0, // your "answer"
            currentInput: 0, // your "numberstring1"
            number: [1, 2, 3, 4, 5, 6, 7, 8, 9],
            numberstring1: 0,
            numberstring2: 0,

            // status definition
            INPUT_LEFT_STATE: 1,
            INPUT_RIGHT_STATE: 2,
            SHOW_ANSWER_STATE: 3,
            CALCULATE_STATE: 4,
            CHANGE_OPERATOR_STATE: 5,

            currentState: 1,


            operation: Function,
        };
    },
    computed: {
        screenValue() {
            if (this.currentState === this.SHOW_ANSWER_STATE
            || this.currentState === this.CALCULATE_STATE
            || this.currentState === this.CHANGE_OPERATOR_STATE
            || this.currentState === this.INPUT_LEFT_STATE) {
                return this.answer;
            }
            return this.currentInput;
        },
    },
    mounted() {
        this.$root.$on("reset-buttons", () => {
            this.clear();
        });
        this.$root.$on("sum-buttons", () => {
            this.onOperater(this.sum);
        });

        this.$root.$on("mul-buttons", () => {
            this.onOperater(this.mul);
        });

        this.$root.$on("equal-buttons", () => {
            this.onEqual();
        });
    },
    methods: {
        inputValue(value) {
            switch (this.currentState) {
                case this.INPUT_LEFT_STATE:
                    this.answer = this.answer * 10 + value;

                    // set next state
                    this.currentState = this.INPUT_LEFT_STATE;
                    break;

                case this.INPUT_RIGHT_STATE:
                    this.currentInput = this.currentInput * 10 + value;

                    // set next state
                    this.currentState = this.INPUT_RIGHT_STATE;
                    break;

                case this.CALCULATE_STATE:
                case this.CHANGE_OPERATOR_STATE:
                    this.currentInput = value;

                    // set next state
                    this.currentState = this.INPUT_RIGHT_STATE;
                    break;


                case this.SHOW_ANSWER_STATE:
                    this.clear();
                    this.answer = value;

                    // set next state
                    this.currentState = this.INPUT_LEFT_STATE;
                    break;

                default:
                    console.log(`unexpect state: ${this.currentState}`);
            }
        },
        onOperater(operation) {
            switch (this.currentState) {
                case this.INPUT_LEFT_STATE:
                    this.operation = operation;

                    // set next state
                    this.currentState = this.INPUT_RIGHT_STATE;
                    break;

                case this.INPUT_RIGHT_STATE:
                    this.answer = this.operation(this.answer, this.currentInput);

                    // set next state
                    this.currentState = this.CALCULATE_STATE;
                    break;


                case this.CALCULATE_STATE:
                case this.CHANGE_OPERATOR_STATE:
                    this.operation = operation;

                    // set next state
                    this.currentState = this.CHANGE_OPERATOR_STATE;
                    break;

                case this.SHOW_ANSWER_STATE:
                    this.operation = operation;

                    // set next state
                    this.currentState = this.CHANGE_OPERATOR_STATE;
                    break;

                default:
                    console.log(`unexpect state: ${this.currentState}`);
            }
        },
        onEqual() {
            switch (this.currentState) {
                case this.INPUT_LEFT_STATE:
                    // set next state
                    this.currentState = this.INPUT_LEFT_STATE;
                    break;

                case this.INPUT_RIGHT_STATE:
                    this.answer = this.operation(this.answer, this.currentInput);

                    // set next state
                    this.currentState = this.SHOW_ANSWER_STATE;
                    break;


                case this.CALCULATE_STATE:
                case this.CHANGE_OPERATOR_STATE:
                case this.SHOW_ANSWER_STATE:
                    // set next state
                    this.currentState = this.SHOW_ANSWER_STATE;
                    break;

                default:
                    console.log(`unexpect state: ${this.currentState}`);
            }
        },
        clear() {
            this.answer = 0;
            this.currentInput = 0;
        },
        sum(leftValue, rightValue) {
            return leftValue + rightValue;
        },
        mul(leftValue, rightValue) {
            return leftValue * rightValue;
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
