<template>
  <div id="app">
      <main class='testerContainer' v-bind:class='{folded: !checked}'>
          <article class="head">
         <div>
    <TesterCheckbox :wrong_guess='this.wrong_guess' :correct_guess='this.correct_guess' />
         </div>
     <div>
         <img class="logo" src='./assets/recaptoba.svg'>
     </div>
          </article>
      <article class='imageGridContainer' v-bind:class='{show: checked}'>
    <ImageGrid @onSubmit='onSubmit($event)' />
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
     correct_guess = false;

    mounted () {
        this.$root.$on('checkbox_checked', (clicked: boolean) => {
            this.checked = clicked;
        })
    }

     onSubmit (event: boolean) {
         if (event) {
             this.onSuccess();
         } else {
             this.setWrongGuess()
         }
     }

    setWrongGuess () {
       if (!this.wrong_guess) {
         this.wrong_guess = true;
             setTimeout(() => {
                 this.wrong_guess = false;
             }, 2000)
        }
     }

     onSuccess () {
         this.correct_guess = true;
         this.checked = false;
         console.log('a winner is you', this.correct_guess)
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

 .logo {
     height: 65px;
     margin: auto;
     padding: 8px;
 }

 .head {
     display: flex;
     justify-content: space-between;
 }

#app {
  font-family: "Roboto", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
    display: flex;
    align-items: center;
    display: flex;
}
</style>
