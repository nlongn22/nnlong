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
                    <home-icon size="1.5x" id="home"></home-icon>
                    Nguyen Ngoc Long
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
                <a href="https://www.instagram.com/nlongn22/" target="_blank">
                    <instagram-icon size="1.5x" class="icon"></instagram-icon>
                </a>
                <a
                    href="https://www.linkedin.com/in/ngoc-long-nguyen-2b0387219/"
                    target="_blank"
                >
                    <linkedin-icon
                        size="1.5x"
                        class="icon"
                        id="linkedin"
                    ></linkedin-icon>
                </a>
                <a href="https://github.com/bobby-22" target="_blank">
                    <github-icon size="1.5x" class="icon"></github-icon
                ></a>
            </div>
        </div>
    </div>
</template>

<script>
import {
    HomeIcon,
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
        HomeIcon,
        InstagramIcon,
        LinkedinIcon,
        GithubIcon,
    },
    methods: {
        jumpToTop() {
            this.$emit("jumpToTop", 0);
        },
    },
};
</script>

<style scoped>
.navbar-container {
    position: fixed;
    z-index: 1;
    width: 100%;
    animation: fade-element 1s;
}
.navbar {
    display: flex;
    justify-content: space-between;
    z-index: 200;
    padding: 30px;
}
.title {
    font-family: "Righteous";
    color: #fbf7f0;
}
#home {
    margin-right: 5px;
}
.name {
    display: flex;
    align-items: center;
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
a:link,
a:visited,
a:active {
    color: inherit;
}
a:link:hover,
a:visited:hover,
a:active:hover {
    color: inherit;
}
</style>
