<template>
    <div class="container">
        <div class="container-left">
            <transition name="fade">
                <div class="header" v-if="message !== '' && isLeft">
                    {{ message }}<span class="cursor">|</span>
                </div>
            </transition>
        </div>
        <div class="container-right">
            <transition name="fade">
                <div class="header" v-if="message !== '' && !isLeft">
                    {{ message }}<span class="cursor">|</span>
                </div>
            </transition>
        </div>
        <div class="scroll-container">
            <div class="scroll">Scroll</div>
            <div class="scroll-icon">
                <i class="fas fa-long-arrow-alt-down"></i>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Home",
    data() {
        return {
            interval: null,
            message: "",
            index: 0,
            isLeft: true,
        };
    },
    methods: {
        initTypewriter(string, isLeft) {
            this.isLeft = isLeft;
            let stringArray = string.split("");
            this.message += stringArray[this.index];
            this.index++;
        },
        initFunction(string, boolean) {
            return new Promise((resolve, reject) => {
                let interval = setInterval(() => {
                    this.initTypewriter(string, boolean);
                    if (this.message === "Willkommen bei meiner Website!") {
                        resolve(this.loopPromises());
                        clearInterval(interval);
                    }
                    if (this.message === string) {
                        this.message = "";
                        this.index = 0;
                        resolve();
                        clearInterval(interval);
                    }
                }, 200);
            });
        },
        loopPromises() {
            this.initFunction("Hello!", true).then(() =>
                this.initFunction("Guten Tag!", false).then(() => {
                    this.initFunction("Welcome to my site!", true).then(() => {
                        this.initFunction(
                            "Willkommen bei meiner Website!",
                            false
                        );
                    });
                })
            );
        },
    },
    mounted() {
        this.loopPromises();
    },
};
</script>

<style>
* {
    font-family: "Righteous";
}
.fade-enter,
.fade-leave-to {
    opacity: 0;
}
.container {
    position: relative;
    display: flex;
    min-height: 100vh;
}
.container-left,
.container-right {
    position: relative;
    flex-basis: 50%;
    padding: 30px;
}
.container-left {
    background-color: #d9e4dd;
}
.container-right {
    background-color: #fbf7f0;
}
.header {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    font-size: 96px;
    transition: 1s;
}
.header::after {
    transition: 1s;
}
.header::before {
    transition: 1s;
}
@keyframes blink {
    0% {
        opacity: 0;
    }
}
.cursor {
    color: #cdc9c3;
    animation: blink 1s steps(2) infinite;
}
.scroll {
    position: absolute;
    top: 90%;
    left: 47.5%;
    transform: rotate(-90deg);
    color: #fbf7f0;
}
.scroll-icon {
    font-size: 24px;
    position: absolute;
    top: 95%;
    left: 50.2%;
    color: #d9e4dd;
}
</style>
