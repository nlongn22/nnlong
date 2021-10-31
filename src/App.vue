<template>
    <div id="container">
        <Navbar v-bind:isHome="isHome" />
        <Home v-if="isHome" />
        <About v-if="isAbout" />
    </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Home from "@/components/Home.vue";
import About from "@/components/About.vue";
export default {
    components: {
        Navbar,
        Home,
        About,
    },
    data() {
        return {
            isHome: true,
            isAbout: false,
        };
    },
    methods: {
        triggerComponent(e) {
            let scrollDistance = e.deltaY;
            console.log(scrollDistance);
            switch (true) {
                case scrollDistance <= -100:
                    this.isHome = true;
                    this.isAbout = false;
                    break;
                case scrollDistance >= 100:
                    this.isHome = false;
                    this.isAbout = true;
                    break;
            }
        },
    },
    mounted() {
        window.addEventListener("wheel", this.triggerComponent);
    },
    beforeDestroy() {
        window.removeEventListener("scroll", this.triggerComponent);
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
