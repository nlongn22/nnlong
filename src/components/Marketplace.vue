<template>
    <div class="container">
        <div class="content-container">
            <div class="header">
                <div>MechMarket.eu</div>
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
        v-bind:currentPage="3"
        v-on:nextPage="jumpToPage"
    />
</template>

<script>
import Scroll from "./Scroll.vue";
import Navigator from "./Navigator.vue";
export default {
    name: "Marketplace",
    components: {
        Scroll,
        Navigator,
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
    display: flex;
    justify-content: space-between;
    align-items: center;
    min-height: 100vh;
    background-color: #fbf7f0;
    animation-name: slide-container-up;
    animation-duration: 1s;
    animation-fill-mode: forwards;
}
.container.back {
    animation-name: slide-container-down;
}
</style>
