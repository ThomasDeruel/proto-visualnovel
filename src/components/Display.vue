<template>
    <div class="displayContainer">
       <div class="text-container">
        <p>{{currentText}}</p>
       </div>

       <div v-if="currentPlayers" class="picturesContainer">
            <img v-for="(player, index) of currentPlayers" 
            :key="'player'+index"
            :style="{marginLeft: player.position+'%'}" 
            :src="getImage(player.picture)">
       </div>

       <div v-if="currentAction" class="actionContainer">
            <router-link
            v-for="(action, index) of currentAction"
            :key="'action'+index"
            :to="{ name: action.redirect}">
                {{action.value}}
            </router-link>
       </div>
    </div>
</template>

<script>
import datajson from '../utils/data/data.json';

export default {
    data(){
        return {
            data:[],
            index:0,
        }
    },
    watch:{
        //on regarde les changements sur le router
        // si c'est le cas, on remet à zéro l'index et on récupère le chapitre en cours
        "$route":"getChapter"
    },
    created(){
        this.getChapter();
    },
    methods: {
       getChapter(){
        console.log('page fin')
        this.index = 0;
        const currentChapter = [...datajson].filter(elem=> elem.name === this.$route.name)[0];
        this.data = currentChapter.data;
       },
       getImage(name) {
           return require('../assets/img/'+name);
       }
    },
    computed:{
        currentText() {
            return this.data[this.index].text;
        },

        currentPlayers() {
            if(this.data[this.index].players !== null) {
                return this.data[this.index].players
            }
            return false;  
        },

        currentAction() {
            if(this.data[this.index].action !== null) {
                return this.data[this.index].action
            }
            return false;              
        }
    }
}
</script>

<style>
.displayContainer {
    position: relative;
    min-height:100%;
    overflow:hidden;
}
.displayContainer .text-container {
    background:rgba(0,0,0,0.7);
    color:white;
    position:absolute;
    z-index:3;
    right:0;
    top:20%;
    width:65%;
    height: 400px;
    padding: 8px;
    text-align:left;
    font-size: 18px;
}
.displayContainer .picturesContainer img {
    position:absolute;
    top:50%;
    left:0;
    z-index:1;
    transform:translateY(-50%);
}

.actionContainer {
    position: absolute;
    z-index: 999999999999;
    bottom: 0;
    margin-bottom: 56px;
    width:100%;
    display:flex;
    justify-content:center;
    width:100%;
}
.actionContainer a {
    color:black;
    width: 250px;
    height: 48px;
    background: white;
    display: flex;
    align-items:center;
    justify-content: center;
    border-radius: 2px;
    text-decoration: none;
    font-weight: bolder;
}
.actionContainer a:not(:first-child) {
    margin-left: 48px;
}
</style>