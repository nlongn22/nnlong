<template>
    <div class="container">
        <div class="container-left">
            <transition name="fade">
                <div class="header" v-if="message !== '' && isLeft">
                    {{ message
                    }}<span
                        class="cursor"
                        v-bind:class="{
                            blinking: message === 'Enjoy your stay!',
                        }"
                        >|</span
                    >
                </div>
            </transition>
            <div class="scroll">Scroll</div>
        </div>
        <div class="container-right">
            <transition name="fade">
                <div class="header" v-if="message !== '' && !isLeft">
                    {{ message }}<span class="cursor">|</span>
                </div>
                <div class="header" v-else-if="message === 'Enjoy your stay!'">
                    <smile-icon size="1.5x" class="smile-icon"></smile-icon>
                </div>
            </transition>
            <arrow-down-icon size="1.5x" class="scroll-icon"></arrow-down-icon>
        </div>
    </div>
</template>

<script>
import { SmileIcon, ArrowDownIcon } from "@zhuowenli/vue-feather-icons";
export default {
    name: "Home",
    components: {
        SmileIcon,
        ArrowDownIcon,
    },
    data() {
        return {
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
        initTypeWriter(string, leftRight) {
            return new Promise((resolve, reject) => {
                setTimeout(() => {
                    let interval = setInterval(() => {
                        this.typeWriter(string, leftRight);
                        if (this.message === "Enjoy your stay!") {
                            resolve();
                            clearInterval(interval);
                            return;
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
                    this.initTypeWriter("Dobrý den!", true).then(() => {
                        this.initTypeWriter("Xin chào!", false).then(() => {
                            this.initTypeWriter("Enjoy your stay!", true);
                        });
                    });
                })
            );
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
    }
    100% {
        flex-basis: 50%;
    }
}
@keyframes slide-right-left {
    0% {
        flex-basis: 100%;
    }
    100% {
        flex-basis: 50%;
    }
}
.container-left,
.container-right {
    position: relative;
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 30px;
    animation: 1s ease-out forwards;
}
.container-left {
    background-color: #d9e4dd;
    animation-name: slide-left-left;
}
.container-right {
    background-color: #fbf7f0;
    animation-name: slide-right-left;
}
.header {
    text-align: center;
    color: #555555;
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
.scroll {
    position: absolute;
    right: 0%;
    transform: rotate(-90deg);
    visibility: hidden;
    margin-right: -7px;
    font-family: "Righteous";
    color: #fbf7f0;
    animation: slide-scroll-down 1s 1s ease-out forwards;
}
@keyframes slide-icon-down {
    0% {
        top: 0%;
    }
    100% {
        visibility: visible;
        top: 93.5%;
    }
}
@keyframes bounce-scroll-icon {
    0% {
        transform: translateY(0px);
    }
    100% {
        transform: translateY(15px);
    }
}
.scroll-icon {
    position: absolute;
    left: 0%;
    visibility: hidden;
    color: #d9e4dd;
    animation: slide-icon-down 1s 1.5s ease-out forwards,
        bounce-scroll-icon 1s cubic-bezier(0.7, 0, 0.3, 1) infinite alternate;
}
.smile-icon {
    animation: fade-element 1s;
}
@keyframes blink {
    0% {
        opacity: 0;
    }
}
.cursor {
    color: #cdc9c3;
}
.cursor.blinking {
    animation: blink 1s steps(2) infinite;
}
</style>
