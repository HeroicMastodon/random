<template>
    <div id="app">
        <week/>
    </div>
</template>

<script lang="ts">
import {Component, Vue} from "vue-property-decorator";
import HelloWorld from "./components/HelloWorld.vue";
import Week from "@/views/Week.vue";

@Component({
    components: {
        HelloWorld,
        Week
    }
})
export default class App extends Vue {}
</script>

<style lang="scss">
html {
    height: 100%;
    width: 100%;
}

body {
    height: 100%;
    width: 100%;
    margin: 0;
    display: inline-block;
}

#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    background-color: #2c3e50;
    height: 100%;
    width: 100%;
}
</style>
