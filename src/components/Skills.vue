<template>
    <div class="container">
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
        <div class="pagination-container">
            <div class="pagination">
                <div class="circle">
                    <div class="current-page">1</div>
                    <div class="all-pages">4</div>
                </div>
                <div class="circle"></div>
                <div class="circle"></div>
                <div class="circle"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Skills",
    methods: {
        triggerComponent(event) {
            let scrollDistance = event.deltaY;
            console.log(scrollDistance);
            switch (true) {
                case scrollDistance >= 100:
                    this.$emit("scrolled", true);
                    break;
                case scrollDistance <= -100:
                    this.$emit("scrolled", false);
            }
        },
    },
    mounted() {
        window.addEventListener("wheel", this.triggerComponent);
    },
    beforeUnmount() {
        window.removeEventListener("wheel", this.triggerComponent);
    },
};
</script>

<style scoped>
@keyframes slide-container-down {
    0% {
        transform: translateY(-100%);
        background-color: #fbf7f0;
    }
    100% {
        transform: translateY(0%);
        background-color: #d9e4dd;
    }
}
.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    min-height: 100vh;
    background-color: #fbf7f0;
    animation-name: slide-container-down;
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
    position: relative;
    height: 10px;
    width: 10px;
    line-height: 10px;
    border-radius: 100%;
    margin-top: 150px;
    background-color: #cdc9c3;
}
.circle:first-child {
    position: relative;
    margin-top: 0px;
    background: none;
    height: 40px;
    width: 40px;
    background: linear-gradient(
        to top left,
        #d9e4dd calc(50% - 1px),
        #cdc9c3,
        #d9e4dd calc(50% + 1px)
    );
}
.all-pages {
    position: absolute;
    bottom: 0px;
    right: 0px;
}
.circle:before {
    content: "";
    position: absolute;
    top: -152px;
    left: 50%;
    height: 280px;
    margin-top: 30px;
    margin-left: -1px;
    border: 1px solid #cdc9c3;
}
.circle:first-child:before {
    display: none;
}
.circle:last-child:before {
    display: none;
}
</style>
