<template>
    <main class="mainWrapper">
        <div class="checkboxContainer">
            <div class="checkboxWrapper">
                <div v-if="!clicked" v-on:click="onClick()" class="checkbox">
                </div>
                <LoadingSpinner v-if="clicked && !wrong_guess" />
                <div v-if="wrong_guess" class="wrong">X</div>
            </div>
            <h3 style="margin-left: 15px; margin-top:20px;">I'm not {{label}}</h3>
        </div>
    </main>
</template>
<script lang="ts">
 import { Component, Prop, Vue } from 'vue-property-decorator';
 import LoadingSpinner from './LoadingSpinner.vue';

 @Component({
     components: {
         LoadingSpinner
     },
 })
 export default class TesterCheckbox extends Vue {


     @Prop({required: false, type: Boolean, default: false})
     wrong_guess: boolean = false;

     srcLabels = [
         "a racist",
         "a sexist",
         "a xenophobe",
         "an ageist",
         "a misogynist",
         "a misandrist",
         "judgmental",
         "predjudiced",
         "biased",
         "an anti-semite"
     ]
     clicked = false;

     label: string = '';

     mounted () {
         this.label = this.pickLabel(this.srcLabels);
     }

     pickLabel (array: any[]): string {
         const label = array[Math.floor(Math.random()*array.length)];
         return 'predjudiced';
     }


     onClick () {
         this.$root.$emit('checkbox_checked', true)
         this.clicked = !this.clicked;
     }
 }
</script>
<style scoped>
 .mainWrapper {
     margin-bottom: 20px;
 }

 .checkbox {
     display: block;
     width: 50%;
     height: 50%;
     cursor: pointer;
     margin: auto;
     font-size: 22px;
     border-radius: 3px;
     border: 3px solid lightgrey;
 }

 .checkboxWrapper {
     display: flex;
     width: 45px;
     height: 45px;
 }

 .checkboxContainer {
     display:flex;
     flex-direction: row;
     align-items: center;
     justify-items: center;
     margin: auto;
     width: 460px;
     height: 100%;
     padding: 10px;
 }

 .wrong {
     text-align: center;
     margin: auto;
     padding-left: 5px;
     font-size: 2.5em;
     font-weight: bolder;
     color: red;
 }
</style>
