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
import Menu from "@/components/Menu.vue";
import Home from "@/views/Home.vue";
import About from "@/views/About.vue";
import Skills from "@/views/Skills.vue";
import Marketplace from "@/views/Marketplace.vue";
export default {
    components: {
        Navbar,
        Menu,
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
@keyframes slide-menu-right {
    0% {
        left: -500px;
    }
    100% {
        left: 30px;
    }
}
#container {
    position: relative;
}
.content-container {
    padding: 114px;
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
.menu-icon {
    position: absolute;
    top: 50%;
    color: #cdc9c3;
    transition: 0.5s;
    animation: slide-menu-right 1s ease-out forwards;
}
.menu-icon:hover {
    cursor: pointer;
    color: #555555;
    transition: 0.5s;
}
</style>
