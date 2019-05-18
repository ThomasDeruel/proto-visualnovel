<template>
  <div class="home">
    <p>{{data[index].name}}</p>
    <div class="">
      <p>{{data[index].text}}</p>
    </div>
    <button v-if="reset" @click="back()">retour au début</button>
    <button v-else @click="next()">suivant</button>
  </div>
</template>

<script>
// @ est un alias de /src
// importation de ton data.json
// grâce à la transpilation (babel) nous pouvons utiliser sans souci
import data from '../utils/data/data.json';

export default {
  name: 'home',
  // data() et non data (cela créerait un state global === A ne pas faire)
  // permet d'encapsuler tes états
  // ici on initialise nos états
  data(){
      return {
        data:[],
        index:0,
      }
  },
  // cycle de vie 'created': au moment où l'instance est crée
  // utile pour les import statiques mais pas que ^^
  created(){
    this.data = data;
  },
  //methods est un objet qui te permet de créer tes fonctions
  methods: {
    next(){
      if(this.index < (data.length-1)) {
         this.index += 1;
      }
    },
    back(){
      this.index = 0;
    }
  },
  //un computed est censé retourner une valeur
  //c'est un observateur, elle oberve les changements d'état
  computed: {
    reset(){
      // si l'index a atteint la fin du tableau: retourne true sinon false
      return this.index === data.length-1;
      /*
        if(this.index === data.length-1) {
          return true
        }
        return false
      */
    }
  }
}
</script>
