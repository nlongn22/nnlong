<template>
    <div class="menu-container">
        <div class="link"></div>
        <div class="link-wrapper" v-if="isShown">
            <div
                class="header"
                v-for="(header, index) in headerArray"
                v-bind:key="header.id"
                v-bind:class="{ current: currentPage === index + 1 }"
                v-on:click="jumpToPage(index + 1)"
            >
                {{ header }}
            </div>
        </div>
        <chevrons-left-icon
            size="3x"
            class="close-icon"
            v-if="isShown"
            v-on:click="closeMenu()"
        ></chevrons-left-icon>
    </div>
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
    data() {
        return {
            headerArray: [
                "About me",
                "Technologies I'm familiar with",
                "MechMarket.eu",
                "Weather-Wizard.xyz",
            ],
            isShown: false,
        };
    },
    methods: {
        closeMenu() {
            this.$emit("closeMenu");
        },
        jumpToPage(pageNumber) {
            this.$emit("jumpToPage", pageNumber);
        },
        showElement() {
            this.isShown = true;
        },
    },
    mounted() {
        setTimeout(() => {
            this.showElement();
        }, 500);
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
    animation: fade-element 0.5s ease-out;
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
@keyframes slide-close-icon-left {
    0% {
        transform: translateX(7px);
    }
    100% {
        visibility: visible;
        transform: translateX(0px);
    }
}
.close-icon {
    margin-left: 30px;
    margin-right: 60px;
    visibility: hidden;
    animation: slide-close-icon-left 1s ease-out forwards,
        fade-element 0.5s ease-out;
}
</style>
