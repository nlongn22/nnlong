<template>
    <div class="container" v-bind:class="{ back: isBack }">
        <div class="content-container">
            <div class="header">
                <div>Technologies I'm familiar with</div>
            </div>
            <div class="text">
                Lorem, ipsum dolor sit amet consectetur adipisicing elit.
                Placeat laborum libero alias saepe ducimus consectetur incidunt
                error laboriosam expedita totam officiis explicabo voluptates
                reiciendis quos, ipsum nihil eveniet sit amet! Lorem ipsum dolor
                sit amet consectetur adipisicing elit. Reiciendis, dolorem. Quas
                debitis earum dolorum quasi modi, ea commodi iusto placeat
                dolores voluptates. Libero eum natus est. Quas doloribus
                obcaecati quibusdam! Lorem ipsum dolor sit amet consectetur
                adipisicing elit. Neque iure obcaecati quaerat doloremque harum
                ipsa repudiandae nulla, blanditiis beatae reiciendis
                consectetur, dicta reprehenderit quis, impedit modi. Magnam amet
                odio ex!
            </div>
        </div>
        <Scroll v-bind:currentPage="2" v-on:jumpToPage="jumpToPage" />
    </div>
    <Navigator
        v-bind:isHidden="false"
        v-bind:currentPage="2"
        v-on:nextPage="jumpToPage"
    />
</template>

<script>
import Scroll from "./Scroll.vue";
import Navigator from "./Navigator.vue";
export default {
    name: "Skills",
    components: {
        Scroll,
        Navigator,
    },
    props: {
        isBack: Boolean,
    },
    methods: {
        jumpToPage(pageNumber) {
            this.$emit("jumpToPage", pageNumber);
        },
    },
};
</script>

<style scoped>
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
.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    min-height: 100vh;
    background-color: #d9e4dd;
    animation-name: slide-container-up;
    animation-duration: 1s;
    animation-fill-mode: forwards;
}
.container.back {
    animation-name: slide-container-down;
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
