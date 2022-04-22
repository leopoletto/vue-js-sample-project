<template>
    <Head title="Fique por dentro" />

    <AuthenticatedLayout>

        <section class="mx-auto sm:w-full sm:px-5 w-1/2 pb-12">
            <h2 class="mb-6 text-white text-center text-[28px] font-bold">Fique por dentro!</h2>

            <Article v-for="(article, index) in news" :key="index" :article="article" class="mb-6" />

            <Pagination />
        </section>
                
    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from '@/Layouts/Authenticated.vue'
import Article from '@/Components/Article.vue';
import Pagination from '@/Components/Pagination.vue';
import { Head } from '@inertiajs/inertia-vue3';

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Article,
        Pagination
    },
    props: {
        news: Array
    },
}
</script>
