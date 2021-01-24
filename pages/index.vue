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
                    <v-img src="images\black.jpg">
                      <v-container fluid wrap fill-height>
                        <v-layout align-center justify-center>
                            <v-img max-width="300px" :src="castedSpell">


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
      openTextModal:false,
      castedSpell:'',
      mensagem:"Você chegou em algum lugar, mas isso não foi programado ainda, avise o bibliotecário que encontrou um lugar estranho."
    }
  },
  methods:{
    checkSpell(){
      switch (this.spell) {
        case 'Ae':
          this.castedSpell="images\\Spells\\ae.gif"
          break;
        case 'Sen':
          this.castedSpell="images\\Spells\\sen.gif"
          break;
        case 'En':
          this.castedSpell="images\\Spells\\en.gif"
          break;
        case 'Pi':
          this.castedSpell="images\\Spells\\pi.gif"
          break;
        case 'Kande':
          this.castedSpell="images\\Spells\\kande.gif"
          break;
        case 'Mite':
          this.castedSpell="images\\Spells\\mite.gif"
          break;
        case 'Tun':
          this.castedSpell="images\\Spells\\tun.gif"
          break;
        case 'For':
          this.castedSpell="images\\Spells\\for.gif"
          break;
        case 'Fot':
          this.castedSpell="images\\Spells\\fot.gif"
          break;
        case 'Awen':
          this.castedSpell="images\\Spells\\awen.gif"
          break;
        default:
          this.mensagem="Isso foi inesperado T.T"
          break;
      }

    },

  },
  computed:{

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

  
</style>