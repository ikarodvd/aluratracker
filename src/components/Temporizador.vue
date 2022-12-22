<template>
    
            <div class="column">
                <cronometro :tempoEmSegundos="tempoEmSegundos"></cronometro>
                <button class="button" @click="iniciar" :disabled="cronometroRodando">
                    <span class="icon"> 
                        <i class="fas fa-play"> </i>
                    </span>
                    <span>play</span>
                </button>
                <button class="button" @click="finalizar" :disabled="!cronometroRodando">
                    <span class="icon"> 
                        <i class="fas fa-stop"> </i>
                    </span>
                    <span>stop</span>
                </button>
            </div>

</template>


<script lang="ts">

    import { defineComponent } from 'vue';
    import Cronometro from './Cronometro.vue';
    export default defineComponent({
        // eslint-disable-next-line vue/multi-word-component-names
        name: 'Temporizador',
        components:{
            Cronometro
        },
        emits: ['aoTemporizadorFinalizado'],
        data(){
            return{
                tempoEmSegundos:0,
                cronometro:0,
                cronometroRodando: false
            }
        },
        computed:{
            tempoDecorrido() :string{
                return new Date(this.tempoEmSegundos*1000).toISOString().substr(11,8)
            }
        },
        methods:{
            iniciar(){
                this.cronometroRodando = true
            this.cronometro = setInterval(()=>{
                this.tempoEmSegundos+=1;
            }, 1000)
            },
            finalizar(){
                clearInterval(this.cronometro)
                this.cronometroRodando = false
                this.$emit('aoTemporizadorFinalizado',this.tempoEmSegundos)
                this.tempoEmSegundos = 0 
            }
        }
    })

</script>
