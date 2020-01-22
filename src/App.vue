<template>
  <div id="app">
      <main class='testerContainer' v-bind:class='{folded: !checked}'>
    <TesterCheckbox :wrong_guess='this.wrong_guess' />
      <article class='imageGridContainer' v-bind:class='{show: checked}'>
    <ImageGrid @onFailedSubmit='setWrongGuess' />
      </article>
      </main>
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
     wrong_guess = false;

    mounted () {
    this.$root.$on('checkbox_checked', (clicked: boolean) => {
    this.checked = clicked;
    console.log('Checkbox chcked', clicked);

    })
    }


     setWrongGuess () {
         if (!this.wrong_guess) {
         this.wrong_guess = true;
             setTimeout(() => {
                 this.wrong_guess = false;
             }, 2000)
         }
     }
 }
</script>

<style>
 .testerContainer {
     margin: auto;
     height: 860px;
     box-shadow: 1px 1px 3px 3px #999;
     transition: all .5s ease-out;
     background-color: #F8F8FF;
     border-radius: 3px;
 }

 .folded {
     height: 80px;
 }

 .imageGridContainer {
     height: 0px;
     transition: all .5s ease-out;
     overflow: auto;
 }

 .show {
     height: 100%;
 }

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
    display: flex;
    align-items: center;
}
</style>
