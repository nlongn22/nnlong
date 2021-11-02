<template>
    <div class="navigator-container" v-bind:class="[changeColor]">
        <div class="wrapper">
            <div class="scroll-top" v-on:click="nextPage(currentPage + 1)">
                <arrow-left-icon
                    size="1.5x"
                    class="down-icon"
                ></arrow-left-icon>
                <div class="direction">Scroll</div>
            </div>
            <div
                class="scroll-bottom"
                v-if="!isHidden"
                v-on:click="nextPage(1)"
            >
                <div class="direction">Top</div>
                <arrow-right-icon
                    size="1.5x"
                    class="up-icon"
                ></arrow-right-icon>
            </div>
        </div>
    </div>
</template>

<script>
import { ArrowLeftIcon, ArrowRightIcon } from "@zhuowenli/vue-feather-icons";
export default {
    name: "Navigator",
    props: {
        isHidden: Boolean,
        currentPage: null,
    },
    data() {},
    components: {
        ArrowLeftIcon,
        ArrowRightIcon,
    },
    computed: {
        changeColor: function () {
            return {
                green: this.currentPage % 2 !== 0,
                white: this.currentPage % 2 === 0,
            };
        },
    },
    methods: {
        nextPage(pageNumber) {
            this.$emit("nextPage", pageNumber);
        },
    },
};
</script>

<style scoped>
.navigator-container {
    position: absolute;
    width: 175px;
    bottom: 0px;
    left: 0px;
    transform: rotate(-90deg) translate(43%, -150%);
    margin-bottom: 30px;
    color: #d9e4dd;
}
.navigator-container.green {
    color: #d9e4dd;
}
.navigator-container.white {
    color: #fbf7f0;
}
.wrapper {
    display: flex;
    justify-content: space-between;
    width: inherit;
}
.scroll-top,
.scroll-bottom {
    display: flex;
    transition: 0.5s;
}
.scroll-top:hover,
.scroll-bottom:hover {
    cursor: pointer;
    color: #555555;
    transition: 0.5s;
}
.direction {
    font-family: "Righteous";
}
.down-icon {
    margin-right: 5px;
}
.up-icon {
    margin-left: 5px;
}
</style>
