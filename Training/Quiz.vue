<template>
    <Head title="Quiz" />

    <AuthenticatedLayout>

        <section class="mx-auto sm:w-full sm:px-5 w-1/2 pb-12">
            <h1 class="text-white text-center text-[28px] font-bold">Quiz</h1>
            <p class="text-white text-sm text-center mb-14 leading-">Escolha a resposta certa, <br> para a pergunta:</p>

            <h2 class="text-white font-bold text-sm mb-6 uppercase text-center">Questão</h2>

            <ul class="flex justify-between mb-8 relative after:w-full after:border-t-2 after:border-yellow-500 after:absolute after:top-2.5">
                <li v-for="(option, index) in question.options" :key="index" class="z-10 border-2 bg-pink-900 border-yellow-500 rounded-full w-6 h-6 relative">
                    <svg v-show="currentQuestion >= index" aria-hidden="true" class="w-4 h-4 absolute left-0.5 top-0.5 text-yellow-500" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
                        <path fill="currentColor" d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z"></path>
                    </svg>
                </li>
            </ul>

            <div class="bg-white py-6 px-7 mx-6 sm:mx-0 rounded-3xl">
                <template v-if="!completed">
                    <h3 class="text-pink-800 text-xs font-xs mb-4 font-bold text-center">{{ question.description }}</h3>

                    <label v-for="(option, index) in question.options" :key="index" :for="'alternative-' + index" class="flex items-center text-pink-800 text-[11px] mb-4">
                        <InputRadio :ref="'alternative-' + index" v-model="choosenAlternative" :value="index" :id="'alternative-' + index" name="alternative" class="outline:none mr-3 appearance-none relative min-w-6 w-6 h-6 border border-pink-800 rounded-full checked:after:bg-pink-800 checked:after:w-4 checked:after:h-4 checked:after:rounded-full checked:after:left-[3px] checked:after:top-[3px] checked:after:absolute "/> 
                        {{ option }}
                    </label>
                </template>
                <template v-else>
                    <img class="mx-auto hidden" src="/images/icon-success.svg" alt="">
                    <img class="mx-auto" src="/images/icon-fail.svg" alt="">

                    <p class="text-pink-800 text-sm mt-7">
                        <strong>Parabéns você acertou <span class="hits">4</span> das <span class="totalQuestions">5</span> questões do Quiz</strong>
                        e está cada vez mais preparado para turbinar suas vendas
                    </p>
                </template>
            </div>

            <div class="flex justify-center mt-12 gap-8">
                <a v-if="!completed" @click.prevent="next" class="appearance-none select-none py-3 px-6 uppercase text-pink-800 bg-yellow-500 cursor-pointer hover:shadow-sm hover:scale-105 transition-transform ease-in-out rounded-full">Enviar resposta</a>
                <Link v-else :href="route('training.index')" class="appearance-none select-none py-3 px-6 uppercase text-pink-800 bg-yellow-500 cursor-pointer hover:shadow-sm hover:scale-105 transition-transform ease-in-out rounded-full">Voltar</Link>
            </div>
        </section>
                
    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from '@/Layouts/Authenticated.vue'
import InputRadio from '@/Components/InputRadio.vue'
import { Head, Link } from '@inertiajs/inertia-vue3'

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Link,
        InputRadio
    },
    props: {
        quiz: Array
    },
    methods: {
        isLast() {
            return (this.currentQuestion + 1) === this.quiz.length
        },
        next(){

            if( this.isLast()  ){
                this.completed = true
                return
            }

            this.currentQuestion++

            this.$refs['alternative-' + this.choosenAlternative].$el.checked = false
            this.choosenAlternative = ''
        }
    },
    data() {
        return {
            currentQuestion: 0,
            choosenAlternative: '',
            completed: false,
        }
    },
    computed: {
        question(){
            return this.quiz[this.currentQuestion]
        }
    }
}
</script>
