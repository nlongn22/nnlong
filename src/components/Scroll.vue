<template>
    <div class="pagination-container">
        <div class="pagination" v-if="currentPage === 1">
            <div class="circle" v-bind:class="{ about: currentPage === 1 }">
                <div class="current-page">1</div>
                <div class="all-pages">4</div>
            </div>
            <div
                class="circle"
                v-bind:class="{ about: currentPage === 1 }"
                v-for="(index, circle) in 3"
                v-bind:key="circle.id"
                v-on:click="jumpToPage(index + 1)"
            ></div>
        </div>

        <div class="pagination" v-if="currentPage === 2">
            <div
                class="circle"
                v-bind:class="{ skills: currentPage === 2 }"
                v-on:click="jumpToPage(1)"
            ></div>
            <div class="circle" v-bind:class="{ skills: currentPage === 2 }">
                <div class="current-page">2</div>
                <div class="all-pages">4</div>
            </div>
            <div
                class="circle"
                v-bind:class="{ skills: currentPage === 2 }"
                v-on:click="jumpToPage(3)"
            ></div>
            <div
                class="circle"
                v-bind:class="{ skills: currentPage === 2 }"
                v-on:click="jumpToPage(4)"
            ></div>
        </div>

        <div class="pagination" v-if="currentPage === 3">
            <div
                class="circle"
                v-bind:class="{ marketplace: currentPage === 3 }"
                v-on:click="jumpToPage(1)"
            ></div>
            <div
                class="circle"
                v-bind:class="{ marketplace: currentPage === 3 }"
                v-on:click="jumpToPage(2)"
            ></div>
            <div
                class="circle"
                v-bind:class="{ marketplace: currentPage === 3 }"
            >
                <div class="current-page">3</div>
                <div class="all-pages">4</div>
            </div>
            <div
                class="circle"
                v-bind:class="{ marketplace: currentPage === 3 }"
                v-on:click="jumpToPage(4)"
            ></div>
        </div>
        <div class="pagination" v-if="currentPage === 4">
            <div
                class="circle"
                v-bind:class="{ weather: currentPage === 4 }"
                v-on:click="jumpToPage(1)"
            ></div>
            <div
                class="circle"
                v-bind:class="{ weather: currentPage === 4 }"
                v-on:click="jumpToPage(2)"
            ></div>
            <div
                class="circle"
                v-bind:class="{ weather: currentPage === 4 }"
                v-on:click="jumpToPage(3)"
            ></div>
            <div class="circle" v-bind:class="{ weather: currentPage === 4 }">
                <div class="current-page">4</div>
                <div class="all-pages">4</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Scroll",
    props: {
        currentPage: null,
    },
    methods: {
        jumpToPage(pageNumber) {
            this.$emit("jumpToPage", pageNumber);
        },
    },
};
</script>

<style scoped>
@keyframes slide-scroll-left {
    0% {
        right: -500px;
    }
    100% {
        right: 30px;
    }
}
.pagination-container {
    position: absolute;
    top: 50%;
    right: 30px;
    transform: translate(125%, -50%);
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    height: 60%;
    margin-right: 50px;
    font-family: "Righteous";
    color: #555555;
    animation: slide-scroll-left 1s ease-out forwards;
}
.pagination {
    display: flex;
    flex-direction: column;
    align-items: center;
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
.circle.about:first-child {
    cursor: auto;
    position: relative;
    margin-top: 0px;
    background: none;
    height: 40px;
    width: 40px;
    background: linear-gradient(
        to top left,
        #fbf7f0 calc(50% - 1px),
        #cdc9c3,
        #fbf7f0 calc(50% + 1px)
    );
}
.circle.about:before {
    content: "";
    position: absolute;
    top: -163px;
    left: 50%;
    height: 310px;
    margin-top: 15px;
    margin-left: -1px;
    border: 1px solid #cdc9c3;
}
.circle.about:first-child:before {
    display: none;
}
.circle.about:last-child:before {
    display: none;
}
.circle.skills:first-child {
    margin-top: 0px;
}
.circle.skills:nth-child(2) {
    cursor: auto;
    height: 40px;
    width: 40px;
    background: linear-gradient(
        to top left,
        #d9e4dd calc(50% - 1px),
        #cdc9c3,
        #d9e4dd calc(50% + 1px)
    );
}
.circle.skills:before {
    content: "";
    position: absolute;
    top: 10px;
    left: 50%;
    height: 500px;
    margin-left: -1px;
    border: 1px solid #cdc9c3;
}
.circle.skills:nth-child(2):before {
    display: none;
}
.circle.skills:nth-child(3):before {
    display: none;
}
.circle.skills:last-child:before {
    display: none;
}
.circle.marketplace:first-child {
    margin-top: 0px;
}
.circle.marketplace:nth-child(3) {
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
.circle.marketplace:before {
    content: "";
    position: absolute;
    top: 10px;
    left: 50%;
    height: 340px;
    margin-left: -1px;
    border: 1px solid #cdc9c3;
}
.circle.marketplace:nth-child(3):before {
    display: none;
}
.circle.marketplace:last-child:before {
    display: none;
}

.circle.weather:first-child {
    margin-top: 0px;
}
.circle.weather:nth-child(4) {
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
.circle.weather:before {
    content: "";
    position: absolute;
    top: 10px;
    left: 50%;
    height: 500px;
    margin-left: -1px;
    border: 1px solid #cdc9c3;
}
.circle.weather:nth-child(2):before {
    display: none;
}
.circle.weather:nth-child(3):before {
    display: none;
}
.circle.weather:last-child:before {
    display: none;
}
</style>
