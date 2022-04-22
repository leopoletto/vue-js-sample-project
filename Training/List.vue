<template>
    <Head title="Capacitação" />

    <AuthenticatedLayout>

        <section class="mx-auto sm:w-full sm:px-5 w-1/2 pb-12">
            <h1 class="text-white text-center text-[28px] font-bold">Capacitação</h1>
            <p class="text-white text-sm text-center mb-14 leading-">Escolha o treinamento, <br> assista e responda o Quiz.</p>

            <TrainingCard class="mb-6" v-for="training in trainings" :training="training" :key="training.id" />
        </section>
                
    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from '@/Layouts/Authenticated.vue'
import TrainingCard from '@/Components/TrainingCard.vue'
import { Head, Link } from '@inertiajs/inertia-vue3'

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Link,
        TrainingCard
    },
    props: {
        trainings: Array
    },
}
</script>
