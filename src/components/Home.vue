<template>
    <div class="container">
        <div class="container-left">
            <transition name="fade">
                <div class="header" v-if="message !== '' && isLeft">
                    {{ message }}<span class="cursor">|</span>
                </div>
            </transition>
            <div class="scroll">Scroll</div>
        </div>
        <div class="container-right">
            <transition name="fade">
                <div class="header" v-if="message !== '' && !isLeft">
                    {{ message }}<span class="cursor">|</span>
                </div>
            </transition>
            <arrow-down-icon size="1.5x" class="scroll-icon"></arrow-down-icon>
        </div>
    </div>
</template>

<script>
import { ArrowDownIcon } from "@zhuowenli/vue-feather-icons";
export default {
    name: "Home",
    components: {
        ArrowDownIcon,
    },
    data() {
        return {
            interval: null,
            message: "",
            index: 0,
            isLeft: true,
        };
    },
    methods: {
        typeWriter(string, isLeft) {
            this.isLeft = isLeft;
            let stringArray = string.split("");
            this.message += stringArray[this.index];
            this.index++;
        },
        initTypeWriter(string, boolean) {
            return new Promise((resolve, reject) => {
                setTimeout(() => {
                    let interval = setInterval(() => {
                        this.typeWriter(string, boolean);
                        if (this.message === "Herzlich Willkommen!") {
                            resolve(this.chainPromises());
                            clearInterval(interval);
                        }
                        if (this.message === string) {
                            this.message = "";
                            this.index = 0;
                            resolve();
                            clearInterval(interval);
                        }
                    }, 175);
                }, 750);
            });
        },
        chainPromises() {
            this.initTypeWriter("Hello!", true).then(() =>
                this.initTypeWriter("Guten Tag!", false).then(() => {
                    this.initTypeWriter("Welcome!", true).then(() => {
                        this.initTypeWriter("Herzlich Willkommen!", false);
                    });
                })
            );
        },
        triggerComponent() {
            this.about = true;
        },
    },
    mounted() {
        setTimeout(() => {
            this.chainPromises();
        }, 2250);
    },
};
</script>

<style scoped>
* {
    font-family: "Righteous";
}
.fade-enter,
.fade-leave-to {
    opacity: 0;
    transition: 0.5s;
}
.container {
    display: flex;
    min-height: 100vh;
}
@keyframes slide-left-left {
    0% {
        flex-basis: 0%;
        background-color: #d9e4dd;
    }
    100% {
        flex-basis: 50%;
        background-color: #d9e4dd;
    }
}
@keyframes slide-left-right {
    0% {
        flex-basis: 100%;
        background-color: white;
    }
    100% {
        flex-basis: 50%;
        background-color: #fbf7f0;
    }
}
.container-left,
.container-right {
    position: relative;
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 30px;
    animation-duration: 1s;
    animation-fill-mode: forwards;
}
.container-left {
    background-color: #d9e4dd;
    animation-name: slide-left-left;
}
.container-right {
    background-color: #fbf7f0;
    animation-name: slide-left-right;
}
.header {
    text-align: center;
    font-size: 96px;
}
@keyframes slide-scroll-down {
    0% {
        top: 0%;
    }
    100% {
        visibility: visible;
        top: 90%;
    }
}
@keyframes slide-icon-down {
    0% {
        top: 0%;
    }
    100% {
        visibility: visible;
        top: 94%;
    }
}
.scroll {
    position: absolute;
    right: 0%;
    transform: rotate(-90deg);
    visibility: hidden;
    margin-right: -7px;
    color: #fbf7f0;
    animation-name: slide-scroll-down;
    animation-duration: 1s;
    animation-delay: 1s;
    animation-fill-mode: forwards;
}
.scroll-icon {
    position: absolute;
    left: 0%;
    visibility: hidden;
    color: #d9e4dd;
    animation: slide-icon-down;
    animation-duration: 1s;
    animation-delay: 1.5s;
    animation-fill-mode: forwards;
}
.cursor {
    color: #cdc9c3;
}
</style>
