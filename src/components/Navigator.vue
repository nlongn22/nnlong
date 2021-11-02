<template>
    <div class="wrapper">
        <div class="scroll-top" v-on:click="nextPage(currentPage + 1)">
            <arrow-left-icon size="1.5x" class="down-icon"></arrow-left-icon>
            <div class="direction">Scroll</div>
        </div>
        <div class="scroll-bottom" v-if="!isHidden" v-on:click="nextPage(1)">
            <div class="direction">Top</div>
            <arrow-right-icon size="1.5x" class="up-icon"></arrow-right-icon>
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
    methods: {
        nextPage(pageNumber) {
            this.$emit("nextPage", pageNumber);
        },
    },
};
</script>

<style scoped>
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
