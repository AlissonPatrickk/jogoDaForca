<template>
    <div class="jogo">

         <Forca
         :erros ="erros"/>   

         <Palavra 
         :palavra="palavra"
         :dica="dica"
         :verificaLetra="verificaLetra"
         :etapa="etapa"
         />

         <Teclado 
         v-if="etapa === 'jogo'"
         :letras="letras"
         :verificaLetra="verificaLetra"
         :jogar="jogar"
         /> 

         <Final 
         v-if="etapa != 'jogo'"
         :etapa="etapa"
         :texto="etapa === 'ganhador' ? 'Carai rogerin tu  é o mais PIK4 !!' : 'Que burro jamelão!'" :jogarNovamente="jogarNovamente"
         />
    
    </div>
</template>

<script>
import Forca from './forca.vue';
import Palavra from './palavra.vue';
import Teclado from './teclado.vue';
import Final from './final.vue'

export default {
    name:'Jogo',
    props:{
        erros:Number,
        palavra: String,
        dica: String,
        verificaLetra: Function,
        etapa: String,
        letras: Array,
        jogar: Function,
        jogarNovamente: Function,

        
    },
    data(){
        return {
            
        }
    },
    methods:{
        
    },
    components:{
        Forca,
        Palavra,
        Teclado,
        Final
    },   
}
</script>

<style>
 .jogo{
     width: 100%;
     display: flex;
     flex-direction: column;
     align-items: center;
     text-align: center;
 }
</style>