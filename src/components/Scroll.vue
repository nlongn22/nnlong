<template>
    <div class="wrapper">
        <div class="scroll-top">
            <arrow-left-icon size="1.5x" class="down-icon"></arrow-left-icon>
            <div class="direction">Scroll</div>
        </div>
        <div class="scroll-bottom">
            <div class="direction">Top</div>
            <arrow-right-icon size="1.5x" class="up-icon"></arrow-right-icon>
        </div>
    </div>
</template>

<script>
import { ArrowLeftIcon, ArrowRightIcon } from "@zhuowenli/vue-feather-icons";
export default {
    name: "Scroll",
    components: {
        ArrowLeftIcon,
        ArrowRightIcon,
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
