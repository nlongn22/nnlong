<template>
    <div class="container" v-bind:class="{ back: isPrevious }">
        <div class="content-container">
            <div class="header" v-if="isShown">
                <div>Technologies I'm familiar with</div>
            </div>
            <div class="text" v-if="isShown">
                Lorem, ipsum dolor sit amet consectetur adipisicing elit.
                Placeat laborum libero alias saepe ducimus consectetur incidunt
                error laboriosam expedita totam officiis explicabo voluptates
                reiciendis quos, ipsum nihil eveniet sit amet! Lorem ipsum dolor
                sit amet consectetur adipisicing elit. Reiciendis, dolorem. Quas
                debitis earum dolorum quasi modi, ea commodi iusto placeat
                dolores voluptates. Libero eum natus est. Quas doloribus
                obcaecati quibusdam! Lorem ipsum dolor sit amet consectetur
                adipisicing elit. Neque iure obcaecati quaerat doloremque harum
                ipsa repudiandae nulla, blanditiis beatae reiciendis
                consectetur, dicta reprehenderit quis, impedit modi. Magnam amet
                odio ex!
            </div>
        </div>
        <Scrollbar v-bind:currentPage="2" v-on:jumpToPage="jumpToPage" />
        <Navigator v-bind:currentPage="2" v-on:nextPage="jumpToPage" />
        <align-left-icon
            size="1.5x"
            class="menu-icon"
            v-on:click="triggerMenu()"
        ></align-left-icon>
        <Menu
            v-if="isOpened"
            v-bind:currentPage="2"
            v-on:closeMenu="triggerMenu"
            v-on:jumpToPage="jumpToPage"
        />
    </div>
</template>

<script>
import { AlignLeftIcon } from "@zhuowenli/vue-feather-icons";
import Scrollbar from "@/components/Scrollbar.vue";
import Menu from "@/components/Menu.vue";
import Navigator from "@/components/Navigator.vue";
export default {
    name: "Skills",
    components: {
        AlignLeftIcon,
        Scrollbar,
        Menu,
        Navigator,
    },
    emits: ["openMenu", "jumpToPage"],
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
.container {
    justify-content: space-between;
    align-items: center;
    background-color: #d9e4dd;
    animation: slide-container-up 1s ease-out forwards;
}
.container.back {
    animation-name: slide-container-down;
}
</style>
