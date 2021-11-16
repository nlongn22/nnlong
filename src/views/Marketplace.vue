<template>
    <div class="container">
        <div class="wrapper-left">
            <img src="@/assets/marketplace/latest.jpeg" v-if="delayEnded" />
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
                            <check-icon
                                size="1x"
                                class="check-icon"
                            ></check-icon>
                            {{ text }}
                        </li>
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
import { AlignLeftIcon, CheckIcon } from "@zhuowenli/vue-feather-icons";
import Scrollbar from "@/components/Scrollbar.vue";
import Menu from "@/components/Menu.vue";
import Navigator from "@/components/Navigator.vue";
export default {
    name: "Marketplace",
    components: {
        AlignLeftIcon,
        CheckIcon,
        Scrollbar,
        Menu,
        Navigator,
    },
    data() {
        return {
            marketplaceTextArray: [
                "Fully-featured marketplace for mechanical keyboards",
                "CRUD operations (Create, Read, Update, Delete posts)",
                "Search posts, review users",
                "Including details, user’s, saved and posts pages ",
                "Supports image upload",
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
    },
    mounted() {
        this.showElement();
        setTimeout(() => {
            this.delayEnded = true;
        }, 1000);
    },
};
</script>

<style scoped></style>
