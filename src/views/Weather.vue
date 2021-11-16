<template>
    <div class="container">
        <div class="wrapper-left" v-bind:class="{ next: isNext }">
            <img src="@/assets/weather/weather.jpeg" v-if="delayEnded" />
        </div>
        <div class="wrapper-right" v-bind:class="{ next: isNext }">
            <div class="wrapper">
                <div class="header" v-if="isShown">
                    <div>
                        <a href="https://weather-wizard.xyz/" target="”_blank”"
                            >Weather-Wizard.xyz</a
                        >
                    </div>
                </div>
                <div class="text" v-if="isShown">
                    <ul>
                        <li
                            v-for="text in weatherTextArray"
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
        <Scrollbar v-bind:currentPage="4" v-on:jumpToPage="jumpToPage" />
        <Navigator
            v-bind:isHidden="false"
            v-bind:currentPage="4"
            v-on:nextPage="jumpToPage"
        />
        <align-left-icon
            size="1.5x"
            class="menu-icon"
            v-on:click="triggerMenu()"
        ></align-left-icon>
        <Menu
            v-if="isOpened"
            v-bind:currentPage="4"
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
    name: "Weather",
    components: {
        AlignLeftIcon,
        CheckIcon,
        Scrollbar,
        Menu,
        Navigator,
    },
    data() {
        return {
            weatherTextArray: [
                "Beautiful & simple weather dashboard",
                "Add any place using Google Maps autocomplete",
                "View current conditions (e. i. humidity, UV indexwind speed and more)",
                "Toggle between hourly and weekly views",
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

<style scoped>
img {
    object-fit: contain;
}
</style>
