<template>
    <div id="container">
        <Navbar v-bind:isHome="page === 0" v-on:jumpToTop="jumpToPage" />
        <Home v-if="page <= 0" v-on:setPageNumber="jumpToPage" />
        <About
            v-if="page === 1"
            v-bind:isBack="isBack"
            v-on:jumpToPage="jumpToPage"
        />
        <Skills
            v-if="page === 2"
            v-bind:isBack="isBack"
            v-on:jumpToPage="jumpToPage"
        />
        <Marketplace
            v-if="page >= 3"
            v-bind:isBack="isBack"
            v-on:jumpToPage="jumpToPage"
        />
    </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Home from "@/components/Home.vue";
import About from "@/components/About.vue";
import Skills from "@/components/Skills.vue";
import Marketplace from "@/components/Marketplace.vue";
export default {
    components: {
        Navbar,
        Home,
        About,
        Skills,
        Marketplace,
    },
    data() {
        return {
            page: 0,
            isBack: false,
        };
    },
    methods: {
        triggerComponent(event) {
            let scrollDistance = event.deltaY;
            switch (true) {
                case scrollDistance > 15:
                    this.isBack = false;
                    this.page += 1;
                    if (this.page >= 3) {
                        this.page = 3;
                    }
                    break;
                case scrollDistance < -15:
                    this.isBack = true;
                    this.page -= 1;
                    if (this.page <= 0) {
                        this.page = 1;
                    }
                    break;
            }
        },
        jumpToPage(pageNumber) {
            if (this.page > pageNumber) {
                this.isBack = true;
            } else {
                this.isBack = false;
            }
            this.page = pageNumber;
        },
    },
    mounted() {
        window.addEventListener("wheel", this.triggerComponent);
    },
    beforeUnmount() {
        window.removeEventListener("wheel", this.triggerComponent);
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
