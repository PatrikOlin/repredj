<template>
    <main class='mainWrapper'>
        <div class='headerContainer'>
            <h2>Select all images with <b>{{taskSelectionItem}}</b></h2>
        </div>
    <div class='gridContainer'>
        <div
            v-for='(image, index) in images'
            :key='image.id'
            class='grid-item clickable'
            v-on:click="imgOnClick(index)"
            v-bind:class="{chosen: image.isChosen}">
            <span class='chosenCheckmark' v-if="image.isChosen"><i class="fas fa-2x fa-check-circle"></i></span>
            <img :src='image.url'/>

        </div>
    </div>
        <div class="tryAgain" v-if="tryAgain">
            <p>Please try again</p>
        </div>
    <div class='footerContainer'>
        <div class='miscButtons'>
            <span v-on:click='onRedo()' class="clickable"><i class="fas fa-lg fa-redo"></i></span>
            <span><i class="fas fa-lg fa-headphones-alt"></i></span>
            <span><i class="fas fa-lg fa-info-circle"></i></span>
        </div>
        <button type="button" v-on:click='onSubmit()'>Verify</button>
    </div>
    </main>
</template>

<script lang="ts">
 import { Component, Prop, Vue } from 'vue-property-decorator';

 @Component
 export default class ImageGrid extends Vue {
     srcImages = [
         {id: 0, isChosen: false, url: 'https://www.placecage.com/c/300/300'},
         {id: 1, isChosen: false, url: 'https://www.placecage.com/c/150/150'},
         {id: 2, isChosen: false, url: 'https://www.placecage.com/c/500/500'},
         {id: 3, isChosen: false, url: 'https://www.placecage.com/g/250/250'},
         {id: 4, isChosen: false, url: 'https://www.placecage.com/c/600/600'},
         {id: 5, isChosen: false, url: 'https://www.placecage.com/c/400/400'},
         {id: 6, isChosen: false, url: 'https://www.placecage.com/g/150/150'},
         {id: 7, isChosen: false, url: 'https://www.placecage.com/c/160/160'},
         {id: 8, isChosen: false, url: 'https://www.placecage.com/c/210/210'},
         {id: 9, isChosen: false, url: 'https://www.placecage.com/c/200/200'},
         {id: 10, isChosen: false, url: 'https://www.placecage.com/c/230/230'},
         {id: 11, isChosen: false, url: 'https://www.placecage.com/c/240/240'},
         {id: 12, isChosen: false, url: 'https://www.placecage.com/c/190/190'},
         {id: 13, isChosen: false, url: 'https://www.placecage.com/c/140/140'},
         {id: 14, isChosen: false, url: 'https://www.placecage.com/c/220/220'},
         {id: 15, isChosen: false, url: 'https://www.placecage.com/c/260/260'},
         {id: 16, isChosen: false, url: 'https://www.placecage.com/c/270/270'},
         {id: 17, isChosen: false, url: 'https://www.placecage.com/c/280/280'},
         {id: 18, isChosen: false, url: 'https://www.placecage.com/c/360/360'},
         {id: 19, isChosen: false, url: 'https://www.placecage.com/c/310/310'},
         {id: 20, isChosen: false, url: 'https://www.placecage.com/c/375/375'},
         {id: 21, isChosen: false, url: 'https://www.placecage.com/c/335/335'},
         {id: 22, isChosen: false, url: 'https://www.placecage.com/c/340/340'},
     ];
     srcTaskSelectionItems = [
         'physical abusers.',
         'criminals.',
         'junkies.',
         'litterers.',
         'sexual deviants.',
         'sinners.',
         'religious fundamentalists.',
         'the mentally ill.',
         'poor people.',
         'rich people.',
        
     ]
     images: any[] = [];
     taskSelectionItem: string = ''
     tryAgain = false;

     mounted () {
         this.randomize();
     }

     shuffleArray (array: any[]): any[] {
         for (let i = array.length - 1; i > 0; i--) {
             const j = Math.floor(Math.random() * (i + 1));
             [array[i], array[j]] = [array[j], array[i]];
         }
         console.log(JSON.parse(JSON.stringify(array)));
         return array;

     }

     pickTaskSelectionItem(array: any[]): any {
         const item = array[Math.floor(Math.random()*array.length)];
         return item;
     }

     onRedo () {
         this.randomize();
     }

     onSubmit () {
         this.randomize();
         this.tryAgain = true;
     }

     randomize () {
        this.clearAllChosen();
        this.images = this.shuffleArray(this.srcImages).slice(0, 9);
         console.log(JSON.parse(JSON.stringify(this.images)));
        this.taskSelectionItem = this.pickTaskSelectionItem(this.srcTaskSelectionItems);
     }

     clearAllChosen () {
         this.srcImages.forEach(img => img.isChosen = false)
     }

     imgOnClick (index: number) {
         this.tryAgain = false;
         this.images[index].isChosen = !this.images[index].isChosen;
     }

 }
</script>

<style scoped>
 .mainWrapper {
     display:flex;
     flex-direction: column;
     align-items: center;
     justify-items: center;
     margin: auto;
     width: 460px;
     padding: 10px;
     background-color: white;
box-shadow: 5px 5px 3px #999;
 }

 .headerContainer {
     width: 100%;
     background-color: #4187df;
     height: 150px;
 }

 .tryAgain {
     margin: auto;
     font-weight: 400;
     color: red;
 }

 .headerContainer h2 {
     padding: 10px;
     color: white;
     font-weight: 300;
     text-align: left
 }

 .headerContainer b {
     font-weight: 800;
 }

 .footerContainer {
     display: flex;
     flex-direction: row;
     width: 100%;
     padding: 25px;
     margin-top: 10px;
     justify-content: space-between;
     box-sizing: border-box;
     border-top: 1px solid lightgrey;
 }

 .footerContainer button {
     background-color: #4187df;
     color: white;
     font-weight: 600;
     padding: 10px 30px 10px 30px;
     border-radius: 5px;
 }

 .miscButtons {
     display: flex;
     flex-direction: row;
     align-items: center;
 }

 .miscButtons span {
     margin-right: 15px;
 }

 .gridContainer {
     display: grid;
     grid-template-columns: repeat(3, 150px);
     grid-template-rows: repeat(3, 150px);
     grid-gap: 5px;
     margin-top: 10px;
 }

 .grid-item {
     width: 100%;
     height: 100%;
     object-fit: cover;
     transition: all .15s ease-out;
 }

 .grid-item img {
     width: 150px;
     height: 150px;
 }

 .chosen {
     transform: scale(.85);
 }

 .chosenCheckmark {
     position: absolute;
     top: 0;
     left: 0;
     color: #4187df;
     background-color: white;
     border-radius: 35px;
 }

 button, .clickable {
     cursor: pointer;
 }



</style>
