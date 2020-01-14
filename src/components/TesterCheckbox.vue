<template>
    <main class="mainWrapper">
        <div class="checkboxContainer">
            <div class="checkBox">
            </div>
            <h3>I'm not {{label}}</h3>
        </div>
    </main>
</template>
<script lang="ts">
 import { Component, Prop, Vue } from 'vue-property-decorator';

 @Component
 export default class TesterCheckbox extends Vue {

     srcLabels = [
         "a racist",
         "a sexist",
         "a xenophobe",
         "an ageist",
         "a misogynist",
         "a misandrist",
     ]

     label: string = '';

     mounted () {
         this.label = this.pickLabel(this.srcLabels);
     }

     pickLabel (array: any[]): string {
         const label = array[Math.floor(Math.random()*array.length)];
         return label;
     }
 }
</script>
<style scoped>
 .mainWrapper {
     margin-bottom: 20px;
 }

 .checkBox {
     display: block;
     width: 20px;
     height: 20px;
     margin-right: 15px;
     margin-bottom: 2px;
     cursor: pointer;
     font-size: 22px;
     border-radius: 3px;
     border: 3px solid lightgrey;
 }

 .checkboxContainer {
     display:flex;
     flex-direction: row;
     align-items: center;
     justify-items: center;
     margin: auto;
     width: 460px;
     padding: 10px;
     background-color: white;
     border-radius: 3px;
     box-shadow: 0px 0px 1px 1px #999;
 }
</style>
