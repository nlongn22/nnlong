<template>
    <div class="container">
        <div class="wrapper-left">
            <img src="@/assets/marketplace/latest.png" v-if="delayEnded" />
        </div>
        <div class="wrapper-right">
            <div class="wrapper">
                <div class="header" v-if="isShown">
                    <div>
                        <a href="https://mechmarket.eu/" target="”_blank”"
                            >MechMarket.eu</a
                        >
                    </div>
                </div>
                <div class="text" v-if="isShown">
                    <ul>
                        <li
                            v-for="text in marketplaceTextArray"
                            v-bind:key="text.id"
                        >
                            {{ text }}
                        </li>
                        <li><u>Technologies:</u> Django; Vue.js, CSS, Bulma</li>
                    </ul>
                </div>
            </div>
        </div>
        <Scrollbar v-bind:currentPage="3" v-on:jumpToPage="jumpToPage" />
        <Navigator v-bind:currentPage="3" v-on:nextPage="jumpToPage" />
        <align-left-icon
            size="1.5x"
            class="menu-icon"
            v-on:click="triggerMenu()"
        ></align-left-icon>
        <Menu
            v-if="isOpened"
            v-bind:currentPage="3"
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
    name: "Marketplace",
    components: {
        AlignLeftIcon,
        Scrollbar,
        Menu,
        Navigator,
    },
    data() {
        return {
            marketplaceTextArray: [
                "Developed a full-stack marketplace for mechanical keyboards",
                "Included CRUD operations (Create, Read, Update and Delete posts)",
                "Implemented authentication (register and login)",
                "Integrated AWS S3 for uploading and deleting images of keyboards",
                "Connected server with client using REST API",
                "Added features such as reviewing sellers, filtering by category, searching by keywords and more",
            ],
            isOpened: false,
            isShown: false,
            delayEnded: false,
        };
    },
    methods: {
        jumpToPage(pageNumber) {
            this.$emit("jumpToPage", pageNumber);
        },
        triggerMenu() {
            this.isOpened = !this.isOpened;
        },
        showElement() {
            if (!this.isPrevious) {
                setTimeout(() => {
                    this.isShown = true;
                }, 1500);
            } else {
                this.isShown = true;
            }
        },
        setTitle() {
            document.title = "MechMarket.eu";
        },
    },
    mounted() {
        this.showElement();
        setTimeout(() => {
            this.delayEnded = true;
        }, 1000);
        this.setTitle();
    },
};
</script>

<style scoped>
li {
    display: list-item;
    list-style-type: circle;
}
</style>
