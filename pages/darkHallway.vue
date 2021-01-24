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
                      <v-text-field v-model='spell' pa-0 ma-0 hide-details label="Diga alguma coisa" max-width='300px' outline>
                      </v-text-field>
                    </v-flex>
                    <v-flex xs3>
                      <v-btn @click="checkSpell()" color="green">></v-btn>
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
                    <v-img v-if='isLightOn' src="images\hallway.png">
                      <v-container fluid wrap fill-height>
                        <v-layout align-center justify-center>
                            <a >
                              <div @click="openTextModal = true" class='textbtn'>

                              </div>
                            </a>
                            <a>
                              <div @click="confirmaModal=true" class='doorbtn'>
                              
                              </div>
                            </a>
                              
                            
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
      confirmaModal:false,
      spell:"",
      text:"'Sob a chama de seu ímpeto, a razão do próprio fim'",
      title:"Você encontra algumas palavras escritas na parede.",
      openTextModal:false,
      isLightOn:false
    }
  },
  methods:{
    checkSpell(){
      switch (this.spell) {
        case 'Ae':
          this.isLightOn=true;
          break;
        case 'AeAe':
          this.isLightOn=false;
      
        default:
          break;
      }

    },
    go(){
      this.$router.push({ path: '/libraryRoom' })
    }

  },
  computed:{
    mensagem(){
      if(this.isLightOn==false){
        return "Está muito difícil de enxergar algo."
      }else{
        return "Você se depara com uma porta ao final do corredor."
      }
    }
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
  width:20%;
  position: absolute;
  height:20%;
  margin-top: -10%;
  margin-left: -20%;
}
.textbtn{
  width:20%;
  margin-top: -15%;
  position: absolute;
  margin-left: 25%;
  height:30px;
}
  
</style>