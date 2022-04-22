<template>
    <Head :title="training.title" />

    <AuthenticatedLayout>

        <section class="mx-auto sm:w-full sm:px-5 w-1/2 pb-12">
            <h2 class="text-white text-center text-[28px] font-bold">Capacitação</h2>
            <p class="text-white text-sm text-center mb-14 leading-">Escolha o treinamento, <br> assista e responda o Quiz.</p>

            <div class="aspect-w-16 aspect-h-9 my-3">
                <iframe :src="training.video" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen=""></iframe>
            </div>


            <h1 class="text-white font-bold text-lg">{{ training.title }}</h1>
            <p class="text-white text-xs my-2.5">{{ training.description }}</p>

            <QuizControls :training="training" :linkTag="false" class="mt-6" />

            <div class="flex justify-center mt-36 gap-8">
                <Link :href="route('training.index')" class="appearance-none select-none py-3 px-6 uppercase text-pink-800 bg-yellow-500 cursor-pointer hover:shadow-sm hover:scale-105 transition-transform ease-in-out rounded-full">Voltar</Link>
                <Link :href="route('training.quiz', training.id)" class="appearance-none select-none py-3 px-6 uppercase text-pink-800 bg-yellow-500 cursor-pointer hover:shadow-sm hover:scale-105 transition-transform ease-in-out rounded-full">Responder</Link>
            </div>
        </section>
                
    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from '@/Layouts/Authenticated.vue'
import QuizControls from '@/Components/QuizControls.vue'
import { Head, Link } from '@inertiajs/inertia-vue3'

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Link,
        QuizControls
    },
    props: {
        training: Object
    },
}
</script>
