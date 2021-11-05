<template>
    <div class="container">
        <div class="wrapper-left">
            <img src="@/assets/weather/weather.jpeg" v-if="delayEnded" />
        </div>
        <div class="wrapper-right">
            <div class="wrapper">
                <div class="header">
                    <div>
                        <a href="https://weather-wizard.xyz/" target="”_blank”"
                            >Weather-Wizard.xyz</a
                        >
                    </div>
                </div>
                <div class="text">
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
        <Scroll v-bind:currentPage="4" v-on:jumpToPage="jumpToPage" />
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
import Scroll from "@/components/Scroll.vue";
import Menu from "@/components/Menu.vue";
import Navigator from "@/components/Navigator.vue";
export default {
    name: "Weather",
    components: {
        AlignLeftIcon,
        CheckIcon,
        Scroll,
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
    },
    mounted() {
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
