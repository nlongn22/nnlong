<template>
    <div class="container">
        <div class="container-left"></div>
        <div class="container-right">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Sequi
            error, quod maxime iusto minima modi explicabo eum dolore ipsum eos
            placeat quia quaerat aliquam dolorem saepe officia, ab hic beatae.
        </div>
    </div>
</template>

<script>
export default {};
</script>

<style scoped>
.container {
    min-height: 100vh;
    display: flex;
}
@keyframes slide-left-left {
    0% {
        flex-basis: 50%;
    }
    100% {
        flex-basis: 0%;
    }
}
@keyframes slide-left-right {
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
    background-color: #fbf7f0;
    animation-name: slide-left-right;
}
</style>
