<template>
    <div class="container" v-bind:class="{ back: isPrevious }">
        <div class="container-left" v-bind:class="{ back: isPrevious }"></div>
        <div class="container-right" v-bind:class="{ back: isPrevious }">
            <div class="content-container">
                <div class="header" v-if="isShown">
                    <div>About me</div>
                </div>
                <p class="text" v-if="isShown">
                    Hey! My name is Ngoc Long Nguyen but most of my friends call
                    me Filip. I'm a full stack web developer who currently lives
                    in Munich, Germany. I am 20 years old and after high school
                    I've decided to take a gap year before entering university
                    to properly learn German. After finishing high school this
                    summer, I decided to start learning the basics of web
                    development. After a few months and a couple of projects,
                    I'm looking for a job in this field either as an intern or a
                    junior developer.
                </p>
                <p class="text" v-if="isShown">
                    In my free time (when I'm not learning anything) I like to
                    read books and hang out with my friends. I'm quite a big fan
                    of Formula 1 so every weekend is spent watching races and
                    following news around this amazing sport. To stay in shape,
                    I try to run at least three times a week to stay healthy and
                    clear my head.
                </p>
            </div>
            <Scrollbar v-bind:currentPage="1" v-on:jumpToPage="jumpToPage" />
        </div>
        <align-left-icon
            size="1.5x"
            class="menu-icon"
            v-on:click="triggerMenu()"
        ></align-left-icon>
        <Menu
            v-if="isOpened"
            v-bind:currentPage="1"
            v-on:closeMenu="triggerMenu"
            v-on:jumpToPage="jumpToPage"
        />
        <Navigator v-bind:currentPage="1" v-on:nextPage="jumpToPage" />
    </div>
</template>

<script>
import { AlignLeftIcon } from "@zhuowenli/vue-feather-icons";
import Scrollbar from "@/components/Scrollbar.vue";
import Menu from "@/components/Menu.vue";
import Navigator from "@/components/Navigator.vue";
export default {
    name: "About",
    components: {
        AlignLeftIcon,
        Scrollbar,
        Menu,
        Navigator,
    },
    props: {
        isPrevious: Boolean,
    },
    data() {
        return {
            isOpened: false,
            isShown: false,
        };
    },
    methods: {
        jumpToPage(pageNumber) {
            this.isOpened = false;
            this.$emit("jumpToPage", pageNumber);
        },
        triggerMenu() {
            this.isOpened = !this.isOpened;
        },
        showElement() {
            if (!this.isPrevious) {
                setTimeout(() => {
                    this.isShown = true;
                }, 1000);
            } else {
                this.isShown = true;
            }
        },
    },
    mounted() {
        this.showElement();
    },
};
</script>

<style scoped>
.container.back {
    animation: slide-container-down 1s ease-out;
}
@keyframes slide-left-left {
    0% {
        width: 50%;
    }
    100% {
        width: 0%;
    }
}
@keyframes slide-right-left {
    0% {
        width: 50%;
    }
    100% {
        width: 100%;
    }
}
.container-left,
.container-right {
    animation: 1s ease-out;
}
.container-left {
    background-color: #d9e4dd;
    animation-name: slide-left-left;
}
.container-right {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #fbf7f0;
    animation-name: slide-right-left;
}
.container-left.back,
.container-right.back {
    animation: none;
}
</style>
