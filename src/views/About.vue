<template>
    <div class="container" v-bind:class="{ back: isPrevious }">
        <div class="container-left" v-bind:class="{ back: isPrevious }"></div>
        <div class="container-right" v-bind:class="{ back: isPrevious }">
            <div class="content-container">
                <div class="header">
                    <div>About me</div>
                </div>
                <div class="text">
                    Lorem, ipsum dolor sit amet consectetur adipisicing elit.
                    Placeat laborum libero alias saepe ducimus consectetur
                    incidunt error laboriosam expedita totam officiis explicabo
                    voluptates reiciendis quos, ipsum nihil eveniet sit amet!
                    Lorem ipsum dolor sit amet consectetur adipisicing elit.
                    Reiciendis, dolorem. Quas debitis earum dolorum quasi modi,
                    ea commodi iusto placeat dolores voluptates. Libero eum
                    natus est. Quas doloribus obcaecati quibusdam!
                </div>
            </div>
            <Scroll v-bind:currentPage="1" v-on:jumpToPage="jumpToPage" />
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
import Scroll from "@/components/Scroll.vue";
import Menu from "@/components/Menu.vue";
import Navigator from "@/components/Navigator.vue";
export default {
    name: "About",
    components: {
        AlignLeftIcon,
        Scroll,
        Menu,
        Navigator,
    },
    props: {
        isPrevious: Boolean,
    },
    data() {
        return {
            isOpened: false,
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
