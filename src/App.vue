<template>
    <div id="container">
        <Navbar v-bind:isHome="page === 0" v-on:jumpToTop="jumpToPage" />
        <Home v-if="page === 0" v-on:setPageNumber="jumpToPage" />
        <About
            v-if="page === 1"
            v-bind:isPrevious="isPrevious"
            v-on:jumpToPage="jumpToPage"
        />
        <Skills
            v-if="page === 2"
            v-bind:isPrevious="isPrevious"
            v-on:jumpToPage="jumpToPage"
        />
        <Marketplace
            v-if="page === 3"
            v-bind:isPrevious="isPrevious"
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
            isPrevious: false,
        };
    },
    methods: {
        triggerComponent(event) {
            let scrollDistance = event.deltaY;
            switch (true) {
                case scrollDistance > 15:
                    this.isPrevious = false;
                    this.page += 1;
                    if (this.page >= 3) {
                        this.page = 3;
                    }
                    break;
                case scrollDistance < -15:
                    this.isPrevious = true;
                    this.page -= 1;
                    if (this.page <= 1) {
                        this.page = 1;
                    }
                    break;
            }
        },
        jumpToPage(pageNumber) {
            if (this.page > pageNumber) {
                this.isPrevious = true;
            } else {
                this.isPrevious = false;
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
@keyframes fade-element {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}
@keyframes slide-container-up {
    0% {
        transform: translateY(100%);
    }
    100% {
        transform: translateY(0%);
    }
}
@keyframes slide-container-down {
    0% {
        transform: translateY(-100%);
    }
    100% {
        transform: translateY(0%);
    }
}
#container {
    position: relative;
}
.content-container {
    padding: 100px;
}
.header {
    margin-bottom: 30px;
    color: #555555;
    font-size: 72px;
    font-family: "Righteous";
}
.text {
    color: #555555;
    font-size: 24px;
    font-family: "ABeeZee";
}
</style>
