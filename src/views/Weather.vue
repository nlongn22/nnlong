<template>
    <div class="container">
        <div class="wrapper-left">
            <a
                href="https://weather-wizard.xyz/"
                title="Go to weather-wizard.xyz"
                target="”_blank”"
                class="image-container"
                @mouseover="this.showLink = true"
                @mouseleave="this.showLink = false"
            >
                <img
                    src="@/assets/weather/home.png"
                    class="project-image"
                    v-if="delayEnded"
                />
                <div class="external-link" v-if="showLink">
                    <external-link-icon size="1.5x"></external-link-icon>
                </div>
            </a>
        </div>
        <div class="wrapper-right">
            <div class="wrapper">
                <div class="header" v-if="isShown">
                    <div>
                        <a
                            href="https://weather-wizard.xyz/"
                            title="Go to weather-wizard.xyz"
                            target="”_blank”"
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
                            {{ text }}
                        </li>
                        <li>
                            <u>Technologies:</u> Google Maps API; Vue.js, CSS
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
import { AlignLeftIcon, ExternalLinkIcon } from "@zhuowenli/vue-feather-icons";
import Scrollbar from "@/components/Scrollbar.vue";
import Menu from "@/components/Menu.vue";
import Navigator from "@/components/Navigator.vue";
export default {
    name: "Weather",
    components: {
        AlignLeftIcon,
        ExternalLinkIcon,
        Scrollbar,
        Menu,
        Navigator,
    },
    data() {
        return {
            weatherTextArray: [
                "Created a beautiful weather dashboard",
                "Implemented Google Maps API for predictive searching of any location",
                "At glance conditions such as humidity, wind speed, UV index, sunrise & sunset, pressure and more",
                "Additional features include filtering by weekly or hourly conditions",
            ],
            isOpened: false,
            isShown: false,
            showLink: false,
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
            document.title = "Weather-Wizard.xyz";
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

<style scoped></style>
