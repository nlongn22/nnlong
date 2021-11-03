<template>
    <transition name="slide" mode="out-in">
        <div class="menu-container">
            <div class="link-wrapper">
                <div
                    class="header"
                    v-bind:class="{ current: currentPage === 1 }"
                    v-on:click="jumpToPage(1)"
                >
                    About me
                </div>
                <div
                    class="header"
                    v-bind:class="{ current: currentPage === 2 }"
                    v-on:click="jumpToPage(2)"
                >
                    Technologies I'm familiar with
                </div>
                <div
                    class="header"
                    v-bind:class="{ current: currentPage === 3 }"
                    v-on:click="jumpToPage(3)"
                >
                    MechMarket.eu
                </div>
                <div
                    class="header"
                    v-bind:class="{ current: currentPage === 4 }"
                    v-on:click="jumpToPage(4)"
                >
                    Weather-Wizard.xyz
                </div>
            </div>
            <chevrons-left-icon
                size="3x"
                class="close-icon"
                v-on:click="closeMenu()"
            ></chevrons-left-icon>
        </div>
    </transition>
</template>

<script>
import { ChevronsLeftIcon } from "@zhuowenli/vue-feather-icons";
export default {
    name: "Menu",
    components: {
        ChevronsLeftIcon,
    },
    props: {
        currentPage: null,
    },
    methods: {
        closeMenu() {
            this.$emit("closeMenu");
        },
        jumpToPage(pageNumber) {
            this.$emit("jumpToPage", pageNumber);
        },
    },
};
</script>

<style scoped>
@keyframes slide-menu-right {
    0% {
        width: 0%;
        background-color: transparent;
    }
    100% {
        width: 100%;
        background-color: #cdc9c3;
    }
}
.menu-container {
    position: absolute;
    min-height: 100%;
    z-index: 999;
    display: flex;
    flex-direction: row-reverse;
    align-items: center;
    animation: slide-menu-right 0.5s ease-out forwards;
}
.link-wrapper {
    min-height: inherit;
    z-index: 999;
    width: inherit;
}
.header.current {
    text-decoration: underline;
    color: black;
}
.header {
    margin: 0px;
    margin-bottom: 30px;
    max-width: 1000px;
}
.header:hover {
    text-decoration: underline;
}
.header,
.close-icon {
    color: #555555;
    transition: 0.5s;
}
.header:hover,
.close-icon:hover {
    cursor: pointer;
    color: black;
    transition: 0.5s;
}
.close-icon {
    margin-left: 30px;
    margin-right: 60px;
}
</style>
