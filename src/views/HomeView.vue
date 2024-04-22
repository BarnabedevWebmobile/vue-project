<script setup>

  // import du composant des cartes
  import perso from '../components/Perso.vue'
  import { onMounted } from "vue";
  import AOS from "aos";

  onMounted(() => {
      AOS.init();
  })
  // import du composant des cartes

</script>

<template>

  <!--zone du logo de la page-->
  <div class="logo">
      <img src="../assets/logo_dragonballapi.webp" alt="logo du site dragonball api">
      <h2>The Dragon Ball API</h2>
  </div>
  <!--zone du logo de la page-->

  <!--zone de combat-->
  <div class="battleroom">
  <!--zone de combat-->
    <h3>
      selection des combatants :
    </h3><br>
    <h4 v-if="localwinner">last winner : {{ localwinner }}</h4><br>
    <!--zone d'affichage des perso-->
    <div class="selected">
    <!--zone d'affichage des perso-->
      
      <!--premier personnage-->
      <div class="char" >
        <div v-if="!battlePerso1"><h4>Perso 1 : </h4></div>

        <!--affichage du personnage variant selon le status de sélection du perso et la victoire-->
        <ul v-if="battlePerso1"><perso :class="{ looser : looserp1}" data-aos="flip-left" data-aos-duration="2000" data-aos-once="false" frombattle="true" class="fighter" :perso="battlePerso1"/></ul>
        <div class="emptydiv" v-if="!battlePerso1"><p class="empty">veuillez selectionner un personnage</p></div>
        <!--affichage du personnage variant selon le status de sélection du perso et la victoire-->
      
      </div>
      <!--premier personnage-->

      <!--boutton de lancement du combat affiché lors d'un combat et non affiché pendant la selection et la victoire-->
      <img class="versus" src="../assets/vs.png" alt="" v-if="battlePerso1 && battlePerso2 && this.winner == ''" v-on:click="fight">
      <!--boutton de lancement du combat affiché lors d'un combat et non affiché pendant la selection et la victoire-->
      <div class="alerte" v-if="selection" v-on:click="hide">
        <p>Des personnages sont déjà selectionné </p>
      </div>
      <!--second personnage-->
      <div class="char" >
        <div v-if="!battlePerso2"><h4>Perso 2 : </h4></div>

        <!--affichage du personnage variant selon le status de sélection du perso et la victoire-->
        <ul v-if="battlePerso2"><perso :class="{ looser : looserp2}" data-aos="flip-right" data-aos-duration="2000" data-aos-once="false" frombattle="true" class="fighter" :perso="battlePerso2"/></ul>
        <div class="emptydiv" v-if="!battlePerso2"><p class="empty">veuillez selectionner un personnage</p></div>
        <!--affichage du personnage variant selon le status de sélection du perso et la victoire-->
      
      </div>
      <!--second personnage-->

    <!--zone d'affichage des perso-->
    </div>
    <!--zone d'affichage des perso-->

    <!--résultat du combat-->
    <div v-if="winner && winner !== 'draw'"><h1>The winner is {{ winner.name }}</h1></div>
    <div v-if="winner && winner == 'draw'"><h1>It's a draw</h1></div>
    <!--résultat du combat-->

  <!--zone de combat-->
  </div>
  <!--zone de combat-->

    <!--erreur en cas de double selection-->
    <div class="error" v-if="btlpbm"><h4>problème lors de la selection du deuxième combatant : un combatant ne peut pas être attribué 2 fois</h4></div>
    <!--erreur en cas de double selection-->
    
    <!--boutton réinitialisant la zone de combat-->
    <button class="reset" v-if="battlePerso1 && battlePerso2" v-on:click="clearbattle">
      clear
    </button>
    <!--boutton réinitialisant la zone de combat-->


    <div class="switchbattle">

        <button v-on:click="this.switchbattle = !this.switchbattle">
          switch
        </button>


        <button v-on:click="autobattle()"> 
          auto select
        </button>

    </div>


  <!--liste de tout les personnages-->
  <div class="allperso">


    <ul class="listeperso" v-if="switchbattle">

      <!--remplissage des cartes avec la mise en forme préparée à part-->
      <perso :perso="perso" data-aos="fade-up" data-aos-anchor-placement="center-bottom" data-aos-duration="1000" frombattle="false" v-on:click="setPerso(perso)" v-for="(perso, index) in Listeperso.items" key="perso" />
      <!--remplissage des cartes avec la mise en forme préparée à part-->

    </ul>


  </div>
  <!--liste de tout les personnages-->
</template>

<script>

// import de l'extension axios
import axios from "axios";
// import de l'extension axios


export default {


  // données vérifier dans le document
  data() {
    return {

      Listeperso: {},
      battlePerso1: '',
      battlePerso2: '',
      btlpbm: false,
      winner: '',
      looserp1: false,
      looserp1: false,
      localwinner: '',
      localperso1: '',
      localperso2: '',
      switchbattle: false,
      randomchar1: '',
      randomchar2: '',
      selection: false

    };
  },
  // données vérifier dans le document

  mounted(){
    this.localwinner = localStorage.getItem('winner')
  },


  // fonctions utilisé dans le dom
  methods: {
    async getAnswer() {
      const { data } = await axios.get("https://dragonball-api.com/api/characters?limit=58");
      this.Listeperso = data;
      console.log(this.Listeperso)
    },

    // ajoute un personnage au combat max 1fois
    setPerso: function(perso){
      if(!this.battlePerso1){
        this.battlePerso1 = perso
        return
      }
      if(this.battlePerso1 && !this.battlePerso2){
        
        if(this.battlePerso1.id === perso.id ){
          this.battlePerso2 = ''
          this.btlpbm = true
          return
        }else{
          this.battlePerso2 = perso
          this.btlpbm = false
          return
        }
      }
    },
    hide(){
      this.selection = false
    },
    // ajoute un personnage au combat max 1fois
    // showperso(){
    //   if(this.switchbattle == false){
    //     this.switchbattle = true
    //   }else{
    //     this.switchbattle = false
    //   }
    // },
    // fonction réinitiallisant les données après un click sur le bouton reset
    clearbattle(){
      this.battlePerso1 = '',
      this.battlePerso2 = '',
      this.winner='',
      this.looserp1 = false,
      this.looserp2 = false,
      this.selection = false
    },
    // fonction réinitiallisant les données après un click sur le bouton reset

    autobattle(){
      this.randomchar1 = Math.floor(Math.random() * (0, 57))
      this.randomchar2 = Math.floor(Math.random() * (0, 57))
      if(this.battlePerso1 && this.battlePerso2){
        this.selection = true
      }else{
        if(this.randomchar1 !== this.randomchar2 && !this.battlePerso1 && !this.battlePerso2){

          this.battlePerso1 = this.Listeperso.items[this.randomchar1]

          this.battlePerso2 = this.Listeperso.items[this.randomchar2]
        }else{
          if(this.battlePerso1 && !this.battlePerso2){
            if(this.battlePerso1.id === this.battlePerso2.id){
              this.randomchar2 = Math.floor(Math.random() * (0, 57))
              this.battlePerso2 = this.Listeperso.items[this.randomchar2]
            }else{
              this.battlePerso2 = this.Listeperso.items[this.randomchar2]
            }

          }
        }
      }
    },

    // fonction gérant les combats et leurs résultat 
    fight(){
      if(this.battlePerso1.ki == this.battlePerso2.ki){
        this.winner = 'draw'
        
        localStorage.setItem('combatant1', this.battlePerso1.name );
          this.localperso1 = localStorage.getItem('combatant1')

          localStorage.setItem('combatant2', this.battlePerso2.name);
          this.localperso2 = localStorage.getItem('combatant2')

          localStorage.setItem('winner', this.winner);
          this.localwinner = localStorage.getItem('winner')
      }else{
        if (this.battlePerso1.ki > this.battlePerso2.ki){
          this.winner = this.battlePerso1
          this.looserp2 = true

          localStorage.setItem('combatant1', this.battlePerso1.name);
          this.localperso1 = localStorage.getItem('combatant1')

          localStorage.setItem('combatant2', this.battlePerso2.name);
          this.localperso2 = localStorage.getItem('combatant2')

          localStorage.setItem('winner', this.winner.name);
          this.localwinner = localStorage.getItem('winner')
        }else{
          this.winner = this.battlePerso2
          this.looserp1 = true
          
          localStorage.setItem('combatant1', this.battlePerso1.name);
          this.localperso1 = localStorage.getItem('combatant1')

          localStorage.setItem('combatant2', this.battlePerso2.name);
          this.localperso2 = localStorage.getItem('combatant2')

          localStorage.setItem('winner', this.winner.name);
          this.localwinner = localStorage.getItem('winner')
        }
        
      }
      console.log(this.localwinner)
    }
    // fonction gérant les combats et leurs résultat 

  },
  // fonctions utilisé dans le dom

  beforeMount() {
    this.getAnswer();
  },
};
</script>

<style>
.logo{
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  padding: 30px;
  font-size: 30px;
  color: rgb(251, 192, 45);
}

.logo img{
  width: 50%;
}

.listeperso{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.listeperso li{
  width: 280px;
  max-height: 800px;
}

.emptydiv{
  height: 95px;
  background-color: #000;
  margin: 50px;
  border-radius: 0.4rem 1.5rem 0.4rem 1.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

.empty{
  text-align: center;
}

.listeperso li, .fighter{
  margin: 0.875rem;
  background-color: rgba(84, 84, 84, 0.65);
  border: 1px solid rgba(84, 84, 84, 0.75);
  list-style: none;
  border-radius: 0.4rem 1.5rem 0.4rem 1.5rem;
}

.versus{
  position: absolute;
  z-index: 1;
  width: 20%;
  margin-left: 30px;
}

.looser{
  display: none .3s;
  opacity: .2;
}

.fighter li{
  width:75%;
}

.content, .fighter content{
  padding: 20px;
}

.listeperso .image, .fighter .image{
  display: flex;
  background-image: url(../assets/89980.webp);
  background-size: cover;
  border-radius: 0.4rem 1.5rem 0rem 0rem;
}

.listeperso .image img{
  height: 250px;
}

.listeperso .image img, .fighter .image img{
  width: auto;
  margin: auto;
  transition: all .3s;
}

.fighter .image img{
  height: 450px;
}

.listeperso .image img:hover{
  transform: scale(1.5);
}

h4, h3{
  color: white;
  font-size: 22px;
}

p{
  padding-left: 30px;
  color: rgb(251, 192, 45);
  font-size: 18px;
}

.error h4{
  color: red;
}

.reset, .switchbattle button{
  background-color: rgb(251, 192, 45);
  width: 120px;
  height: 30px;
  border: 0;
  border-radius: 0.5rem;
  font-size: 20px;
  margin: 15px;
}

.switchbattle{
  display: flex;
  justify-content: center;
}

.selected{
  display: flex;
  margin-bottom: 50px;
  justify-content: center;
  align-items: center;
}

h1{
  text-align: center;
  color: aliceblue;
}

.char{
  width: 50%;
}

.char ul{
  padding-left: 0;
}
.alerte{
  position: absolute;
  z-index: 1;
  background-color: #6c757d;
  color: #e9ecef;
  border: 1px solid #343a40;
  border-radius: 3rem;
  width: 500px;
  height: 120px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
@media ( max-width: 1039px ) {
  .listeperso li{
    width: 45%;
  }
}

@media (max-width: 880px) {
  .listeperso li{
    width: 40%
  }
}

@media (max-width: 575px) {
  .listeperso li{
    width: 80%
  }
}
</style>