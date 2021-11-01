<template>
    <div id="container">
        <Navbar v-bind:isHome="isHome" />
        <Home v-if="isHome" v-on:scrolled="switchToAbout" />
        <About
            v-if="isAbout"
            v-on:scrolled="switchToSkills"
            v-bind:isBack="isBack"
        />
        <Skills v-if="isSkills" v-on:scrolled="switchToProject" />
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
