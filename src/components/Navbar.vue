<template>
    <div class="navbar-container">
        <div class="navbar">
            <div
                class="title"
                v-bind:style="[
                    isHome
                        ? { color: '#fbf7f0' }
                        : {
                              color: '#cdc9c3',
                          },
                ]"
            >
                <div class="name" v-on:click="jumpToTop()">
                    Ngoc Long Nguyen
                </div>
            </div>
            <div
                class="links"
                v-bind:style="[
                    isHome
                        ? { color: '#d9e4dd' }
                        : {
                              color: '#cdc9c3',
                          },
                ]"
            >
                <instagram-icon size="1.5x" class="icon"></instagram-icon>
                <linkedin-icon
                    size="1.5x"
                    class="icon"
                    id="linkedin"
                ></linkedin-icon>
                <github-icon size="1.5x" class="icon"></github-icon>
            </div>
        </div>
    </div>
</template>

<script>
import {
    InstagramIcon,
    LinkedinIcon,
    GithubIcon,
} from "@zhuowenli/vue-feather-icons";
export default {
    name: "Navbar",
    props: {
        isHome: Boolean,
    },
    components: {
        InstagramIcon,
        LinkedinIcon,
        GithubIcon,
    },
    methods: {
        jumpToTop() {
            this.$emit("jumpToTop", 1);
        },
    },
};
</script>

<style scoped>
* {
    font-family: "Righteous";
}
@keyframes fade-container {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}
.navbar-container {
    position: fixed;
    z-index: 1;
    width: 100%;
    animation-name: fade-container;
    animation-duration: 1s;
}
.navbar {
    display: flex;
    justify-content: space-between;
    z-index: 200;
    padding: 30px;
}
.title {
    color: #fbf7f0;
}
.name {
    transition: 0.5s;
}
.links {
    text-align: right;
    color: #d9e4dd;
    transition: 0.5s;
}
.name:hover,
.icon:hover {
    cursor: pointer;
    color: #555555;
    transition: 0.5s;
}
#linkedin {
    margin-left: 15px;
    margin-right: 15px;
}
</style>
