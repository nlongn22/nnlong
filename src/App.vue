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
        <Marketplace v-if="page === 3" v-on:jumpToPage="jumpToPage" />
        <Weather v-if="page === 4" v-on:jumpToPage="jumpToPage" />
    </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Menu from "@/components/Menu.vue";
import Home from "@/views/Home.vue";
import About from "@/views/About.vue";
import Skills from "@/views/Skills.vue";
import Marketplace from "@/views/Marketplace.vue";
import Weather from "@/views/Weather.vue";
export default {
    components: {
        Navbar,
        Menu,
        Home,
        About,
        Skills,
        Marketplace,
        Weather,
    },
    data() {
        return {
            page: 0,
            isPrevious: false,
            timestamp: null,
        };
    },
    methods: {
        getTimestamp() {
            let minutes = new Date().getMinutes();
            let seconds = new Date().getSeconds();
            let miliseconds = new Date().getMilliseconds();
            let fullTime = seconds * 1000 + minutes * 60000 + miliseconds;
            return fullTime;
        },
        triggerComponent(event) {
            if (this.getTimestamp() - this.timestamp <= 500) {
                return;
            } else {
                this.timestamp = this.getTimestamp();
            }
            let scrollDistance = event.deltaY;
            switch (true) {
                case scrollDistance > 0:
                    this.isPrevious = false;
                    this.page += 1;
                    if (this.page >= 4) {
                        this.page = 4;
                    }
                    break;
                case scrollDistance < 0:
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
        this.timestamp = this.getTimestamp();
    },
    beforeUnmount() {
        window.removeEventListener("wheel", this.triggerComponent);
    },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Righteous&display=swap");
@import url("https://fonts.googleapis.com/css2?family=ABeeZee&display=swap");
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
.container {
    position: relative;
    display: flex;
    min-height: 100vh;
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
@keyframes slide-menu-right {
    0% {
        left: -500px;
    }
    100% {
        left: 30px;
    }
}
.menu-icon {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    color: #cdc9c3;
    transition: 0.5s;
    animation: slide-menu-right 1s ease-out forwards;
}
.menu-icon:hover {
    cursor: pointer;
    color: #555555;
    transition: 0.5s;
}
.check-icon {
    margin-right: 15px;
    color: #cdc9c3;
}
@keyframes fade-element {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}
img {
    height: 100%;
    width: 100%;
    border-radius: 5px;
    animation: fade-element 0.5s ease-out;
}
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}
li {
    display: flex;
    align-items: flex-start;
    margin-bottom: 25px;
}
a:link,
a:visited,
a:active {
    text-decoration: none;
    color: #555555;
    transition: 0.5s;
}
a:link:hover,
a:visited:hover,
a:active:hover {
    color: black;
    text-decoration: underline;
    transition: 0.5s;
}

@keyframes slide-wrapper-left {
    0% {
        width: 100%;
    }
    100% {
        width: 50%;
    }
}
@keyframes slide-wrapper-right {
    0% {
        width: 0%;
    }
    100% {
        width: 50%;
    }
}
@keyframes padding {
    0% {
        padding: 0px;
    }
    100% {
        padding: 114px;
    }
}
.wrapper-left,
.wrapper-right {
    position: relative;
    display: flex;
    justify-content: space-around;
    align-items: center;
}
.wrapper-left {
    background-color: #d9e4dd;
    animation: slide-wrapper-left 1s ease-out forwards,
        padding 0.3s 1s ease-out forwards;
}
.wrapper-right {
    background-color: #fbf7f0;
    animation: slide-wrapper-right 1s ease-out forwards,
        padding 0.3s 1s ease-out forwards;
}
</style>
