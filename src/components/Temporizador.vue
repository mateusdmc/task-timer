<template>
    <div class="is-flex is-align-items-center is-justify-content-center is-flex-grow-3">
        <Cronometro :tempoEmSegundos="tempoEmSegundos"/>
        <button class="button esp" @click="iniciar" :disabled="cronometroRodando"><span class="icon"><i class="fas fa-play"></i></span><span>play</span></button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando"><span class="icon"><i class="fas fa-stop"></i></span><span>stop</span></button>
    </div>
</template>

<script lang="ts">
    import { defineComponent } from 'vue'
    import Cronometro from './Cronometro.vue'

    export default defineComponent({
        name: 'TemporizadorTarefa',
        emits: ['aoTemporizadorFinalizado'],
        components: {
            Cronometro
        },
        data (){
            return{
                tempoEmSegundos: 0,
                cronometro: 0, 
                cronometroRodando: false
            }
        },
        methods: {
            iniciar (){
                // Começa a contagem
                this.cronometroRodando = true
                this.cronometro = setInterval(() => {
                    this.tempoEmSegundos += 1
                }, 1000)
                console.log('iniciando...');
            },
            finalizar (){
                // Fiinaliza a contagem
                this.cronometroRodando = false
                clearInterval(this.cronometro)
                this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
                this.tempoEmSegundos = 0
                console.log('finlizando...');
            }
        }
    })
</script>

<style>
.esp{
    margin-left: 20px;
    margin-right: 20px;
}
</style>