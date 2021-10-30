<template>
    <div class="container">
        <div class="container-left">
            <div class="header">Hello</div>
        </div>
        <div class="container-right">
            <div class="header">Guten Tag</div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Home",
};
</script>

<style>
.container {
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
    font-family: "Righteous";
    font-size: 96px;
    text-align: center;
}
</style>
