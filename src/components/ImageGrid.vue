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
            <span class='chosenCheckmark' v-if="image.isChosen">
                <i class="fas fa-2x fa-check-circle"></i></span>
            <img :src='image.url'/>
        </div>
    </div>
    <div class='footerContainer'>
        <div class='miscButtons'>
            <span v-on:click='onRedo()' class="clickable"><i class="fas fa-lg fa-redo"></i></span>
            <span v-on:click='playAudio()' class="clickable"><i class="fas fa-lg fa-headphones-alt"></i></span>
            <span><i class="fas fa-lg fa-info-circle"></i></span>
        </div>
        <div class="tryAgain" v-bind:class="{hidden: !tryAgain}">
            <p>Please try again</p>
        </div>
        <button type="button" v-on:click='onSubmit()'>Verify</button>
    </div>
    </main>
</template>

<script lang="ts">
 import { Component, Prop, Vue, Emit } from 'vue-property-decorator';
 import { Howl } from 'howler';

 @Component
 export default class ImageGrid extends Vue {
     srcImages = [
         {id: 0, isChosen: false, url: require('@/assets/img/person.jpg')},
         {id: 1, isChosen: false, url:  require('@/assets/img/person(1).jpg')},
         {id: 2, isChosen: false, url:  require('@/assets/img/person(2).jpg')},
         {id: 3, isChosen: false, url:  require('@/assets/img/person(3).jpg')},
         {id: 4, isChosen: false, url:  require('@/assets/img/person(4).jpg')},
         {id: 5, isChosen: false, url:  require('@/assets/img/person(5).jpg')},
         {id: 6, isChosen: false, url:  require('@/assets/img/person(6).jpg')},
         {id: 7, isChosen: false, url:  require('@/assets/img/person(7).jpg')},
         {id: 8, isChosen: false, url:  require('@/assets/img/person(8).jpg')},
         {id: 9, isChosen: false, url:  require('@/assets/img/person(9).jpg')},
         {id: 10, isChosen: false, url:  require('@/assets/img/person(10).jpg')},
         {id: 11, isChosen: false, url:  require('@/assets/img/person(11).jpg')},
         {id: 12, isChosen: false, url:  require('@/assets/img/person(12).jpg')},
         {id: 13, isChosen: false, url:  require('@/assets/img/person(13).jpg')},
         {id: 14, isChosen: false, url:  require('@/assets/img/person(14).jpg')},
         {id: 15, isChosen: false, url:  require('@/assets/img/person(15).jpg')},
         {id: 16, isChosen: false, url:  require('@/assets/img/person(16).jpg')},
         {id: 18, isChosen: false, url:  require('@/assets/img/person(18).jpg')},
         {id: 19, isChosen: false, url:  require('@/assets/img/person(19).jpg')},
         {id: 20, isChosen: false, url:  require('@/assets/img/person(20).jpg')},
         {id: 21, isChosen: false, url:  require('@/assets/img/person(21).jpg')},
         {id: 22, isChosen: false, url:  require('@/assets/img/person(22).jpg')},
         {id: 23, isChosen: false, url:  require('@/assets/img/person(23).jpg')},
         {id: 24, isChosen: false, url:  require('@/assets/img/person(24).jpg')},
         {id: 25, isChosen: false, url:  require('@/assets/img/person(25).jpg')},
         {id: 26, isChosen: false, url:  require('@/assets/img/person(26).jpg')},
         {id: 27, isChosen: false, url:  require('@/assets/img/person(27).jpg')},
         {id: 28, isChosen: false, url:  require('@/assets/img/person(28).jpg')},
         {id: 29, isChosen: false, url:  require('@/assets/img/person(29).jpg')},
         {id: 30, isChosen: false, url:  require('@/assets/img/person(30).jpg')},
         {id: 31, isChosen: false, url:  require('@/assets/img/person(31).jpg')},
         {id: 32, isChosen: false, url:  require('@/assets/img/person(32).jpg')},
         {id: 33, isChosen: false, url:  require('@/assets/img/person(33).jpg')},
         {id: 34, isChosen: false, url:  require('@/assets/img/person(34).jpg')},
         {id: 35, isChosen: false, url:  require('@/assets/img/person(35).jpg')},
         {id: 36, isChosen: false, url:  require('@/assets/img/person(36).jpg')},
         {id: 37, isChosen: false, url:  require('@/assets/img/person(37).jpg')},
         {id: 38, isChosen: false, url:  require('@/assets/img/person(38).jpg')},
         {id: 39, isChosen: false, url:  require('@/assets/img/person(39).jpg')},
         {id: 40, isChosen: false, url:  require('@/assets/img/person(40).jpg')},
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
         'child abusers.',
         'perverts.',
         'heathens.',
         'thieves.',
         'bad parents.',
         'homosexuals.',
         'bisexuals.',
         'asexuals.',
         'heterosexuals.',
         'foreigners.',
         'atheists.',
         'satanists.',
         'christians.',
         'muslims.',
         'buddhists.',
         'jews.',
         'poor drivers.',
         'alcoholics.'
        
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
         return array;
     }

     pickTaskSelectionItem(array: any[]): any {
         const item = array[Math.floor(Math.random()*array.length)];
         return item;
     }

     onRedo () {
         this.randomize();
     }

     @Emit('onSubmit')
     onSubmit () {
         let success = false;
         if (this.images.some(img => img.isChosen)) {
         this.randomize();
         this.tryAgain = true;
         } else {
             success = true;
         }
         return success;
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

     playAudio () {
         let sound = new Howl({
             src:require('@/assets/audio/madonna_wtf.mp3'),
             volume: 0.5,
         });
         sound.play()
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
 }

 .triangle {
     width: 0;
     height: 0;
     border-color: transparent white;
     border-style: solid;
     border-width: 20px 20px 20px 0px;
     position: absolute;
     top: 57%;
     margin-left: -15px;
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
     visibility: visible;
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
     color: white;
     font-weight: 600;
     padding: 10px 30px 10px 30px;
     border-radius: 5px;
     background-color: #4187df;
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

 .visible {
     visibility: visible;
 }

 .hidden {
     visibility: hidden;
 }



</style>
