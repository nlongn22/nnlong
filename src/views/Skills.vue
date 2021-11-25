<template>
    <div class="container" v-bind:class="{ back: isPrevious }">
        <div class="content-container">
            <div class="header" v-if="isShown">
                <div>Technologies I'm familiar with</div>
            </div>
            <div class="text" v-if="isShown">
                <div class="languages">
                    <ul>
                        <li><i class="fab fa-python"></i>Python</li>
                        <li><i class="fab fa-js-square"></i>Javascript</li>
                        <li><i class="fab fa-css3-alt"></i>CSS</li>
                        <li><i class="fab fa-html5"></i>HTML</li>
                    </ul>
                </div>
                <div class="frameworks">
                    <ul>
                        <li><i class="fab fa-python"></i>Django</li>
                        <li><i class="fab fa-vuejs"></i>Vue.js</li>
                        <li>
                            <i class="fab fa-bootstrap"></i>Bootstrap, Bulma
                        </li>
                    </ul>
                </div>
                <div class="others">
                    <ul>
                        <li><i class="fas fa-database"></i>SQL</li>
                        <li><i class="fas fa-server"></i>REST API</li>
                    </ul>
                </div>
                <div class="techniques">
                    <ul>
                        <li><i class="fab fa-git"></i>Git & Github</li>
                        <li><i class="fab fa-aws"></i>AWS S3</li>
                    </ul>
                </div>
            </div>
        </div>
        <Scrollbar v-bind:currentPage="2" v-on:jumpToPage="jumpToPage" />
        <Navigator v-bind:currentPage="2" v-on:nextPage="jumpToPage" />
        <align-left-icon
            size="1.5x"
            class="menu-icon"
            v-on:click="triggerMenu()"
        ></align-left-icon>
        <Menu
            v-if="isOpened"
            v-bind:currentPage="2"
            v-on:closeMenu="triggerMenu"
            v-on:jumpToPage="jumpToPage"
        />
    </div>
</template>

<script>
import { AlignLeftIcon } from "@zhuowenli/vue-feather-icons";
import Scrollbar from "@/components/Scrollbar.vue";
import Menu from "@/components/Menu.vue";
import Navigator from "@/components/Navigator.vue";
export default {
    name: "Skills",
    components: {
        AlignLeftIcon,
        Scrollbar,
        Menu,
        Navigator,
    },
    emits: ["openMenu", "jumpToPage"],
    props: {
        isPrevious: Boolean,
    },
    data() {
        return {
            isOpened: false,
            isShown: false,
        };
    },
    methods: {
        jumpToPage(pageNumber) {
            this.isOpened = false;
            this.$emit("jumpToPage", pageNumber);
        },
        triggerMenu() {
            this.isOpened = !this.isOpened;
        },
        showElement() {
            if (!this.isPrevious) {
                setTimeout(() => {
                    this.isShown = true;
                }, 1000);
            } else {
                this.isShown = true;
            }
        },
        setTitle() {
            document.title = "Technologies";
        },
    },
    mounted() {
        this.showElement();
        this.setTitle();
    },
};
</script>

<style scoped>
.container {
    justify-content: space-between;
    align-items: center;
    background-color: #d9e4dd;
    animation: slide-container-up 1s ease-out forwards;
}
.container.back {
    animation-name: slide-container-down;
}
.text {
    display: flex;
    justify-content: space-between;
}
li {
    display: flex;
    align-items: center;
}
i {
    margin-right: 10px;
}
</style>
