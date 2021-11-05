<template>
    <div class="navigator-container" v-bind:class="changeColor">
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
    components: {
        ArrowLeftIcon,
        ArrowRightIcon,
    },
    computed: {
        changeColor: function () {
            return {
                green: this.currentPage === 1,
                white:
                    this.currentPage === 2 ||
                    this.currentPage === 3 ||
                    this.currentPage === 4,
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
    color: #d9e4dd;
    animation: slide-navigator-up 1s ease-out forwards;
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
