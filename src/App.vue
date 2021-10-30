<template>
    <div id="container">
        <Navbar />
        <router-view />
    </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
export default {
    components: {
        Navbar,
    },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Righteous&display=swap");
@import url("https://fonts.googleapis.com/css2?family=ABeeZee&display=swap");
#container {
    position: relative;
}
</style>
