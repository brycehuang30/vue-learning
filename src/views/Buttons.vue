<template>
    <div class="buttons">
        <div>{{ doorStatus }}</div>
        <div>
            <ClickCountButton
                msg="開門"
                @click.native="open"
            />
            <ClickCountButton
                msg="關門"
                @click.native="close"
            />
            <ClickCountButton
                msg="鎖門"
                @click.native="lock"
            />
            <ClickCountButton
                msg="解鎖"
                @click.native="unlock"
            />
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

            currentStatus: 0,

            // 設定state, 通常就是從0開始編流水號,
            // 我們只要讓每個STATE對應到的號碼不同就好了
            DOOR_OPEN_STATE: 0,
            DOOR_CLOSE_STATE: 1,
            DOOR_HALF_STATE: 2,
            DOOR_LOCKED_STATE: 3,
        };
    },
    computed: {
        doorStatus() {
            // 根據目前的狀態顯示文字
            switch (this.currentStatus) {
                case this.DOOR_OPEN_STATE:
                    return "門開著";

                case this.DOOR_CLOSE_STATE:
                    return "門關著";

                case this.DOOR_HALF_STATE:
                    return "門半開著";

                case this.DOOR_LOCKED_STATE:
                    return "門鎖著";

                default:
                    return "Error";
            }
        },
    },
    methods: {
        open() {
            switch (this.currentStatus) {
                case this.DOOR_OPEN_STATE:
                case this.DOOR_HALF_STATE:
                    this.currentStatus = this.DOOR_OPEN_STATE;
                    break;

                case this.DOOR_CLOSE_STATE:
                    this.currentStatus = this.DOOR_HALF_STATE;
                    break;

                case this.DOOR_LOCKED_STATE:
                    this.currentStatus = this.DOOR_LOCKED_STATE;
                    break;

                default:
                    console.log(`unexpected state${this.currentStatus}`);
            }
        },
        close() {
            switch (this.currentStatus) {
                case this.DOOR_OPEN_STATE:
                    this.currentStatus = this.DOOR_HALF_STATE;
                    break;

                case this.DOOR_CLOSE_STATE:
                case this.DOOR_HALF_STATE:
                    this.currentStatus = this.DOOR_CLOSE_STATE;
                    break;

                case this.DOOR_LOCKED_STATE:
                    this.currentStatus = this.DOOR_LOCKED_STATE;
                    break;

                default:
                    console.log(`unexpected state${this.currentStatus}`);
            }
        },
        lock() {
            // TODO: 補上做lock action的狀態轉換
            switch (this.currentStatus) {
                case this.DOOR_CLOSE_STATE:
                case this.DOOR_LOCKED_STATE:
                    this.currentStatus = this.DOOR_LOCKED_STATE;
                    break;
                case this.DOOR_OPEN_STATE:
                    this.currentStatus = this.DOOR_OPEN_STATE;
                    break;
                case this.DOOR_HALF_STATE:
                    this.currentStatus = this.DOOR_HALF_STATE;
                    break;

                default:
                    console.log(`unexpected state${this.currentStatus}`);
            }
        },
        unlock() {
            // TODO: 補上做unlock action的狀態轉換
            switch (this.currentStatus) {
                case this.DOOR_CLOSE_STATE:
                    this.currentStatus = this.DOOR_CLOSE_STATE;
                    break;
                case this.DOOR_LOCKED_STATE:
                    this.currentStatus = this.DOOR_CLOSE_STATE;
                    break;
                case this.DOOR_OPEN_STATE:
                    this.currentStatus = this.DOOR_OPEN_STATE;
                    break;
                case this.DOOR_HALF_STATE:
                    this.currentStatus = this.DOOR_HALF_STATE;
                    break;

                default:
                    console.log(`unexpected state${this.currentStatus}`);
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

    div {
        display: flex;
        flex-direction: row;
        justify-content: center;

    }
}
</style>
