<template>
    <v-card flat class='elevation-0' max-width='600px'>
        <v-card-title>
            {{title}}
        </v-card-title>
        <v-card-text>
            {{text}}
        </v-card-text>
    </v-card>
</template>
<script>
export default {
    props:['title', 'text'],
    data(){
        return{

        }
    }
}
</script>