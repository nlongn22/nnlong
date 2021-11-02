<template>
    <div id="container">
        <Navbar v-bind:isHome="isHome" v-on:clicked="switchToHome" />
        <Home v-if="isHome" v-on:scrolled="switchToAbout" />
        <About
            v-if="isAbout"
            v-bind:isBack="isBack"
            v-on:scrolled="switchToSkills"
            v-on:clicked="switchComponent"
        />
        <Skills
            v-if="isSkills"
            v-on:scrolled="switchToProject"
            v-on:clicked="switchComponent"
        />
    </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Home from "@/components/Home.vue";
import About from "@/components/About.vue";
import Skills from "@/components/Skills.vue";
export default {
    components: {
        Navbar,
        Home,
        About,
        Skills,
    },
    data() {
        return {
            isHome: true,
            isAbout: false,
            isSkills: false,
            isBack: false,
        };
    },
    methods: {
        switchComponent(pageNumber) {
            console.log(pageNumber === 2);
            switch (true) {
                case pageNumber === 1:
                    this.isAbout = true;
                    this.isBack = true;
                    this.isSkills = false;
                    break;
                case pageNumber === 2:
                    this.isAbout = false;
                    this.isSkills = true;
                    break;
            }
        },
        switchToHome() {
            this.isHome = true;
            this.isAbout = false;
            this.isSkills = false;
            this.isBack = false;
        },
        switchToAbout(boolean) {
            switch (true) {
                case boolean:
                    this.isHome = false;
                    this.isAbout = true;
                    this.isBack = false;
                    this.isSkills = false;
                    break;
            }
        },
        switchToSkills(boolean) {
            switch (true) {
                case boolean:
                    this.isHome = false;
                    this.isAbout = false;
                    this.isSkills = true;
                    break;
                case !boolean:
                    this.isHome = true;
                    this.isAbout = false;
                    this.isSkills = false;
                    break;
            }
        },
        switchToProject(boolean) {
            switch (true) {
                case boolean:
                    this.isHome = false;
                    this.isAbout = false;
                    this.isSkills = true;
                    break;
                case !boolean:
                    this.isHome = false;
                    this.isAbout = true;
                    this.isBack = true;
                    this.isSkills = false;
                    break;
            }
        },
    },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Righteous&display=swap");
@import url("https://fonts.googleapis.com/css2?family=ABeeZee&display=swap");
#container {
    position: relative;
}
</style>
