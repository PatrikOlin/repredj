<template>
    <main class="mainWrapper">
        <div class="checkboxContainer">
            <div class="checkboxWrapper">
                <div v-if="!clicked" v-on:click="onClick()" class="checkbox">
                </div>
                <LoadingSpinner v-if="clicked" />
            </div>
            <h3 style="margin-left: 15px; padding-top:3px;">I'm not {{label}}</h3>
        </div>
    </main>
</template>
<script lang="ts">
 import { Component, Prop, Vue } from 'vue-property-decorator';
 import LoadingSpinner from './LoadingSpinner.vue';

 @Component({
     components: {
         LoadingSpinner
     }
 })
 export default class TesterCheckbox extends Vue {

     srcLabels = [
         "a racist",
         "a sexist",
         "a xenophobe",
         "an ageist",
         "a misogynist",
         "a misandrist",
     ]
     clicked = false;

     label: string = '';

     mounted () {
         this.label = this.pickLabel(this.srcLabels);
     }

     pickLabel (array: any[]): string {
         const label = array[Math.floor(Math.random()*array.length)];
         return label;
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
     background-color: #F8F8FF;
     border-radius: 3px;
     box-shadow: 0px 0px 1px 1px #999;
     transition: height 10s ease-out;
 }
</style>
