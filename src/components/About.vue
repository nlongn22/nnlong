<template>
    <div class="container" v-bind:class="{ back: isPrevious }">
        <div class="container-left" v-bind:class="{ back: isPrevious }"></div>
        <div class="container-right" v-bind:class="{ back: isPrevious }">
            <div class="content-container">
                <div class="header">
                    <div>About me</div>
                </div>
                <div class="text">
                    Lorem, ipsum dolor sit amet consectetur adipisicing elit.
                    Placeat laborum libero alias saepe ducimus consectetur
                    incidunt error laboriosam expedita totam officiis explicabo
                    voluptates reiciendis quos, ipsum nihil eveniet sit amet!
                    Lorem ipsum dolor sit amet consectetur adipisicing elit.
                    Reiciendis, dolorem. Quas debitis earum dolorum quasi modi,
                    ea commodi iusto placeat dolores voluptates. Libero eum
                    natus est. Quas doloribus obcaecati quibusdam!
                </div>
            </div>
            <Scroll v-bind:currentPage="1" v-on:jumpToPage="jumpToPage" />
        </div>
        <Navigator
            v-bind:isHidden="true"
            v-bind:currentPage="1"
            v-on:nextPage="jumpToPage"
        />
    </div>
</template>

<script>
import Scroll from "./Scroll.vue";
import Navigator from "./Navigator.vue";
export default {
    name: "About",
    components: {
        Scroll,
        Navigator,
    },
    props: {
        isPrevious: Boolean,
    },
    methods: {
        jumpToPage(pageNumber) {
            this.$emit("jumpToPage", pageNumber);
        },
    },
};
</script>

<style scoped>
.container {
    position: relative;
    display: flex;
    min-height: 100vh;
}
.container.back {
    animation-name: slide-container-down;
    animation-duration: 1s;
}
@keyframes slide-left-left {
    0% {
        flex-basis: 50%;
    }
    100% {
        flex-basis: 0%;
    }
}
@keyframes slide-right-left {
    0% {
        flex-basis: 50%;
    }
    100% {
        flex-basis: 100%;
    }
}
.container-left,
.container-right {
    animation-duration: 1s;
}
.container-left {
    background-color: #d9e4dd;
    animation-name: slide-left-left;
}
.container-right {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #fbf7f0;
    animation-name: slide-right-left;
}
.container-left.back,
.container-right.back {
    animation-name: none;
}
</style>
