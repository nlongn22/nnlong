<template>
    <div class="navigator-container">
        <div class="wrapper">
            <div
                class="scroll-top"
                v-if="currentPage !== 4"
                v-on:click="nextPage(currentPage + 1)"
            >
                <arrow-left-icon
                    size="1.5x"
                    class="down-icon"
                ></arrow-left-icon>
                <div class="direction">Scroll</div>
            </div>
            <div
                class="scroll-bottom"
                v-if="currentPage !== 1"
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
        currentPage: null,
    },
    components: {
        ArrowLeftIcon,
        ArrowRightIcon,
    },
    methods: {
        nextPage(pageNumber) {
            this.$emit("nextPage", pageNumber);
        },
    },
};
</script>

<style scoped>
@keyframes slide-navigator-up {
    0% {
        top: 500%;
    }
    100% {
        top: 94%;
        visibility: visible;
    }
}
.navigator-container {
    position: absolute;
    width: 175px;
    left: 30px;
    transform: rotate(-90deg) translate(43%, -325%);
    margin-bottom: 30px;
    visibility: hidden;
    color: #cdc9c3;
    animation: slide-navigator-up 1s ease-out forwards;
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
@keyframes bounce-scroll-icon {
    0% {
        transform: translateX(0px);
    }
    100% {
        transform: translateX(15px);
    }
}
.down-icon {
    margin-right: 20px;
    animation: bounce-scroll-icon 1s 1s cubic-bezier(0.7, 0, 0.3, 1) infinite
        alternate;
}
.up-icon {
    margin-left: 5px;
}
</style>
