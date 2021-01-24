<template>
  <v-container fluid pa-0 ma-0>
    <div class='dark'>
      <v-layout pa-0 fill-height>
        <v-flex pa-0 xs12>
          
            <v-container fluid>
              <v-layout fill-height row wrap justify-center>
                
                <v-flex xs4>
                  <v-layout justify-space-around row wrap align-center>
                    <v-flex xs8>
                      <v-text-field :disabled="!playingPuzzle" v-model='spell' pa-0 ma-0 hide-details label="Diga alguma coisa" max-width='300px' outline>
                      </v-text-field>
                    </v-flex>
                    <v-flex xs3>
                      <v-btn :disabled="!playingPuzzle" @click="checkSpell()" color="green">></v-btn>
                    </v-flex>
                    
                  </v-layout>
                  
                </v-flex>
                <v-flex xs12>
                  <div class='tall'>
                    <v-layout row wrap>
                      <v-flex xs12 text-xs-center>
                        <p>{{mensagem}}</p>
                      </v-flex>
                    </v-layout>
                    <v-img v-if="playingPuzzle==false" src="images\libraryRoom.png">
                      <v-container fluid wrap fill-height>
                        <v-layout align-center justify-center>
                            <a v-if="hasKey">
                                <div @click="confirmaModal=true" class='doorbtn'></div>
                            </a>
                            <a >
                                <div @click="playingPuzzle=true; mensagem='Ao se aproximar da mesa, você encontra três velas estranhamente alinhadas'" class="textbtn">
                                    
                                </div>
                            </a>
                            <a v-if="hasKey">
                                <div @click="openHiddenModal=true" class="hiddenbtn">
                                    
                                </div>
                            </a>
                        </v-layout>

                      </v-container>
                    </v-img>
                    <v-img v-else src="images\mesa.png">
                      <v-container fluid wrap fill-height>
                        
                        <v-layout align-end justify-center>
                            <p @click="playingPuzzle=false; mensagem='A sala parece uma bagunça, com diversas pequenas mesinhas repletas de livros. A porta está trancada.'" class='headline'>Voltar</p>
                            <v-img @click="openTextModal=true" v-if="blueCandle=='blueCandleRaised'" class='blueCandle' max-width='100px' contain src="images\note.png">

                            </v-img>
                            <v-img @click="hasKey=true" v-if="greenCandle=='greenCandleRaised' && !hasKey" class='greenCandle' max-width='100px' contain src="images\key.png">

                            </v-img>
                            <v-img @click="raiseCandle('blue')" :class='blueCandle' max-width='100px' contain :src="litCandles.blue">

                            </v-img>
                            
                            <v-img @click="raiseCandle('green')" :class='greenCandle' max-width='100px' contain :src="litCandles.green">

                            </v-img>
                            <v-img @click="raiseCandle('red')" :class='redCandle' max-width='100px' contain :src="litCandles.red">

                            </v-img>
                            
                        </v-layout>

                      </v-container>
                    </v-img>
                  </div>
                </v-flex>
                
              </v-layout>
            </v-container>
          
        </v-flex>
      </v-layout>
    </div>
    <v-layout justify-center row wrap>
        <v-dialog max-width="600" v-model="openTextModal">
          <text-modal :text='text' :title='title'  />
        </v-dialog>
      
    </v-layout>
    <v-layout justify-center row wrap>
        <v-dialog max-width="600" v-model="openHiddenModal">
          <text-modal :text='hiddenText' :title='hiddenTitle'  />
        </v-dialog>
      
    </v-layout>
    <v-layout justify-center row wrap>
        <v-dialog max-width="600" v-model="confirmaModal">
          <modal-confirma @close="confirmaModal=false" @confirm="go()"  />
        </v-dialog>
      
    </v-layout>
  </v-container>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'
import TextModal from '~/components/TextModal.vue'
import ModalConfirma from '../components/ModalConfirma.vue'

export default {
  components: {
    Logo,
    VuetifyLogo,
    TextModal,
    ModalConfirma
  },
  data(){
    return{
      openHiddenModal:false,
      confirmaModal:false,
      spell:"",
      text:"'Sua fome insaciável e seu traje carmesim'",
      title:"Você encontra uma nota, com uma mensagem escrita.",
      hiddenText:"Perseguia sua luz, mas habitava o seu breu",
      hiddenTitle:"Ao vasculhar os livros da biblioteca, você encontra um papel sujo de sangue, com as palavras:",
      openTextModal:false,
      hasKey:false,
      blueCandle:"blueCandle",
      redCandle:"redCandle",
      greenCandle:"greenCandle",
      playingPuzzle:false,
      candlesAreLit:false,
      mensagem:"A sala parece uma bagunça, com diversas pequenas mesinhas repletas de livros. A porta está trancada."
    }
  },
  methods:{
    checkSpell(){
      switch (this.spell) {
        case 'Ae':
          this.candlesAreLit=true;
          break;
        case 'AeAe':
          this.candlesAreLit=false;
          break;
        default:
          this.mensagem="Isso foi inesperado T.T"
          break;
      }

    },
    go(){
        this.$router.push({ path: '/' })
    },
    raiseCandle(whichOne){
        if(this.candlesAreLit == false){
            return
        }
        switch (whichOne) {
            case "red":
                if(this.redCandle == 'redCandle'){
                    this.redCandle = 'redCandleRaised'

                }else{
                    this.redCandle = 'redCandle'
                }
                break;
            case "green":
                if(this.greenCandle == 'greenCandle'){
                    this.greenCandle = 'greenCandleRaised'

                }else{
                    this.greenCandle = 'greenCandle'
                }
                
                break;
            case "blue":
                if(this.blueCandle == 'blueCandle'){
                    this.blueCandle = 'blueCandleRaised'

                }else{
                    this.blueCandle = 'blueCandle'
                }
                
                break;
        
            default:
                break;
        }

    }

  },
  computed:{
    litCandles(){
        if(this.candlesAreLit ==true){
            return {
                green:"images\\litgreen.png",
                red:"images\\litred.png",
                blue:"images\\litblue.png",
            }
        }else{
            return {
                green:"images\\vela verde.png",
                red:"images\\vela vermelha.png",
                blue:"images\\vela azul.png",
            }
        }
    },

  }
}
</script>
<style>

.dark{
  background-color: black;
}
.tall{
  height:1300px;
}
.doorbtn{
  width:10%;
  position: absolute;
  height:30%;
  margin-left: -40%;
  margin-top: -10%;

}
.textbtn{
  width:20%;
  height: 15%;
  margin-top: 5%;
  position: absolute;
  margin-left: 30%;
}
.hiddenbtn{
  width:5%;
  height: 5%;
  margin-top: -20%;
  position: absolute;
  margin-left: 30%;
}

.redCandle{
    position: absolute;

    margin-bottom: 10%;
}
.greenCandle{
    position: absolute;
    margin-left:25%;
    margin-bottom: 10%;
}
.blueCandle{
    position: absolute;
    margin-right:25%;
    margin-bottom: 10%;
}

.redCandleRaised{
    position: absolute;

    margin-bottom: 15%;
}
.greenCandleRaised{
    position: absolute;
    margin-left:25%;
    margin-bottom: 15%;
}
.greenCandle{
    position: absolute;
    margin-left:25%;
    margin-bottom: 10%;
}
.blueCandle{
    position: absolute;
    margin-right:25%;
    margin-bottom: 10%;
}
.blueCandleRaised{
    position: absolute;
    margin-right:25%;
    margin-bottom: 15%;
}
  
</style>