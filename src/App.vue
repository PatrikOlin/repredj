<template>
  <div id="app">
    <TesterCheckbox class='testerContainer' />
    <ImageGrid class='imageGridContainer' v-bind:class='{show: checked}'/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "./components/HelloWorld.vue";
import ImageGrid from "./components/ImageGrid.vue";
import TesterCheckbox from "./components/TesterCheckbox.vue";

@Component({
  components: {
    HelloWorld,
    ImageGrid,
    TesterCheckbox,
  }
})
export default class App extends Vue {

    checked = false;

    mounted () {
    this.$root.$on('checkbox_checked', (clicked: boolean) => {
    this.checked = clicked;
    console.log('Checkbox chcked', clicked);

    })
    }
 }
</script>

<style>
 .testerContainer {
     height: 60px;
     margin: auto;
 }

 .imageGridContainer {
     visibility: hidden;
     transition: all .5s ease-out;
 }


 .show {
     visibility: visible;
 }

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
