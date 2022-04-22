<template>
    <Head :title="article.title" />

    <AuthenticatedLayout>

        <section class="mx-auto sm:w-full sm:px-5 w-1/2 pb-12">
            <h2 class="mb-6 text-white text-center text-[28px] font-bold">Fique por dentro!</h2>

            <picture class="w-full h-52 bg-white items-center justify-center flex mr-3 mb-4">
                <img :src="article.image" alt="" class="w-full h-full object-contain">
            </picture>
            
            <h1 class="text-white font-bold text-lg">{{ article.title }}</h1>

            <Link class="text-yellow-500 flex mt-20 text-sm">
                <svg class="w-5 h-5 mr-2 justify-center items-center" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="download" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
                    <path fill="currentColor" d="M216 0h80c13.3 0 24 10.7 24 24v168h87.7c17.8 0 26.7 21.5 14.1 34.1L269.7 378.3c-7.5 7.5-19.8 7.5-27.3 0L90.1 226.1c-12.6-12.6-3.7-34.1 14.1-34.1H192V24c0-13.3 10.7-24 24-24zm296 376v112c0 13.3-10.7 24-24 24H24c-13.3 0-24-10.7-24-24V376c0-13.3 10.7-24 24-24h146.7l49 49c20.1 20.1 52.5 20.1 72.6 0l49-49H488c13.3 0 24 10.7 24 24zm-124 88c0-11-9-20-20-20s-20 9-20 20 9 20 20 20 20-9 20-20zm64 0c0-11-9-20-20-20s-20 9-20 20 9 20 20 20 20-9 20-20z"></path>
                </svg>
                Baixe o arquivo complementar!
            </Link>

            <div class="flex justify-center mt-16">
                <Link :href="route('news.index')" class="appearance-none select-none py-4 px-6 mx-auto text-xs font-normal text-center text-pink-800 bg-yellow-500 cursor-pointer hover:shadow-sm hover:scale-105 transition-transform ease-in-out rounded-full">Voltar</Link>
            </div>
        </section>
                
    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from '@/Layouts/Authenticated.vue'
import { Head, Link } from '@inertiajs/inertia-vue3';

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Link,
    },
    props: {
        article: Object
    },
}
</script>
