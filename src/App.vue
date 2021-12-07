<template>
  <div id="app">
    <h1> Jogo da forca</h1>

    <section v-if="tela === 'inicio'" id="inicio">
      <Formulario v-if="etapa === 'palavra'"
      title="Defina a palavra"
      button="Proximo"
      :action="setPalavra"
      />
      
      

      <Formulario v-if="etapa === 'dica'"
      title="Defina a dica"
      button="Iniciar o jogo:"
      :action="setDica"
      />

    </section>

    <section v-if="tela === 'jogo'" id="jogo">
      
      <Jogo 
        :erros="erros"
        :palavra="palavra"
        :dica="dica"
        :verificaLetra="verificaLetra"
        :etapa="etapa"
        :letras="letras"
        :jogar="jogar"
        :jogarNovamente="jogarNovamente"
      />
      

    </section>

  </div>
</template>

<script>
import './css/global.css';
import Formulario from './components/formulario.vue';
import Jogo from './components/jogo.vue';


export default {
  name: 'App',
  data(){
    return{
      tela: 'inicio',
      etapa: 'palavra',
      palavra:'',
      dica:'',
      erros: 0,
      letras: []
      }
  },
  components: {
    Formulario,
    Jogo,    
  },
  methods:{
    setPalavra: function(palavra){
      this.palavra = palavra;
      this.etapa = 'dica';
    },
    setDica: function(dica){
      this.dica = dica;
      this.tela = 'jogo';
      this.etapa = 'jogo';
    },

    verificaLetra: function(letra){
      return this.letras.find(item => item.toLowerCase() === letra.toLowerCase());
    },

    jogar: function(letra){     
      this.letras.push(letra);

      this.verificaErro(letra);
    },
    verificaErro: function(letra){
      if(this.palavra.toLowerCase().indexOf(letra.toLowerCase()) >= 0) {
        return this.verificaAcerto();

      }
      this.erros++;
      if(this.erros === 6){
        this.etapa = 'enforcado'
      }
    },
    verificaAcerto: function(){
      let letraUnica = [...new Set (this.palavra.split(''))];
      if(letraUnica.length === (this.letras.length - this.erros)){
        this.etapa = 'ganhador';
      }
    },
    jogarNovamente: function(){
      this.palavra = '';
      this.dica = '';
      this.erros = 0;
      this.letra =[];
      this.tela = 'inicio';
      this.etapa = 'palavra'
      
    }
  }
}
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
