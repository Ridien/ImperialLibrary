<template>
    <v-card flat class='elevation-0' max-width='600px'>
        
        <v-card-title>
            Tem Certeza? Explore mais um pouco
        </v-card-title>
        <v-container fluid>
            <v-layout justify-end>
                <v-btn mr-2 color="error" @click="$emit('close')">
                    Voltar
                </v-btn>
                <v-btn ml-2 color="success" @click="$emit('confirm')">
                    Tenho.
                </v-btn>
            </v-layout>
        </v-container>
        
        

    </v-card>
</template>
<script>
export default {
    data(){
        return{

        }
    }
}
</script>