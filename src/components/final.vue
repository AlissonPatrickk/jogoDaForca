<template>
    <div class="final">
        <div :class="`final-texto ${etapa}`">
            {{texto}}
        </div>

        <button class="final-botao" v-on:click="reloadPage">Jogar novamente</button>
      </div>    
</template>

<script>

export default {
    name: 'final',
    props:{
        etapa: String,
        texto: String,
        jogarNovamente: Function
    },
    data(){
        return {
            
        }
    },
    methods:{
        reloadPage() {
      window.location.reload();
    }
    },
    component:{

    }
}
</script>

<style>
.final-texto{
    margin:20px 0px;
    font-size: 24px;
    font-weight: bold;
}
.final-texto.enforcado{
    color:var(--color-text-error);
}
.final-texto.ganhador{
    color:var(--color-text-sucess);
}

</style>