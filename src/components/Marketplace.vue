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
        <div class="pagination-container">
            <div class="pagination">
                <div class="circle" v-on:click="jumpToPage(1)"></div>
                <div class="circle">
                    <div class="current-page">2</div>
                    <div class="all-pages">4</div>
                </div>
                <div class="circle" v-on:click="jumpToPage(3)"></div>
                <div class="circle" v-on:click="jumpToPage(4)"></div>
            </div>
        </div>
    </div>
    <div class="scroll-container">
        <Navigator
            v-bind:isHidden="false"
            v-bind:currentPage="3"
            v-on:nextPage="jumpToPage"
        />
    </div>
</template>

<script>
import Navigator from "./Navigator.vue";
export default {
    name: "Marketplace",
    components: {
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
@keyframes slide-container-up {
    0% {
        transform: translateY(100%);
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
    background-color: #fbf7f0;
    animation-name: slide-container-up;
    animation-duration: 1s;
    animation-fill-mode: forwards;
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
.pagination-container {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    height: 60%;
    margin-right: 50px;
    font-family: "Righteous";
    color: #555555;
}
.pagination {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.circle {
    cursor: pointer;
    position: relative;
    height: 10px;
    width: 10px;
    line-height: 10px;
    border-radius: 100%;
    margin-top: 150px;
    background-color: #cdc9c3;
}
.circle:first-child {
    margin-top: 0px;
}
.circle:nth-child(2) {
    cursor: auto;
    height: 40px;
    width: 40px;
    background: linear-gradient(
        to top left,
        #fbf7f0 calc(50% - 1px),
        #cdc9c3,
        #fbf7f0 calc(50% + 1px)
    );
}
.circle:before {
    content: "";
    position: absolute;
    top: 10px;
    left: 50%;
    height: 500px;
    margin-left: -1px;
    border: 1px solid #cdc9c3;
}
.circle:nth-child(2):before {
    display: none;
}
.circle:nth-child(3):before {
    display: none;
}
.circle:last-child:before {
    display: none;
}
.current-page,
.all-pages {
    font-size: 18px;
}
.all-pages {
    position: absolute;
    bottom: 0px;
    right: 0px;
}
.scroll-container {
    position: absolute;
    width: 175px;
    bottom: 0px;
    left: 0px;
    transform: rotate(-90deg) translate(43%, -150%);
    margin-bottom: 30px;
    color: #d9e4dd;
}
</style>
