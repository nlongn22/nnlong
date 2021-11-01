<template>
    <div class="container">
        <div class="container-left"></div>
        <div class="container-right">
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
    </div>
</template>

<script>
export default {
    name: "About",
};
</script>

<style scoped>
.container {
    display: flex;
    min-height: 100vh;
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
    animation-fill-mode: forwards;
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
        #fbf7f0 calc(50% - 1px),
        #cdc9c3,
        #fbf7f0 calc(50% + 1px)
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
