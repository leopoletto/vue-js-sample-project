<template>
    <Head title="Terms" />
    <HeaderComponent :showExtras="false" />
    <div>
        <Heading title="Privacidade" />
        <div class="p-4 px-5">
          <p class="text-[20px] pb-[25px]">Saiba como tratamos os seus dados:</p>
          <article class="text-gray-800 pb-[22px]">
            <Wysiwyg v-for="article in articles" :key="article.title" :title="article.title" :text="article.text" />
          </article>
        </div>
        <FooterComponent />
    </div>
</template>

<script>
import { Head } from '@inertiajs/inertia-vue3';
import Heading from '@/Components/UI/Texts/Heading.vue'
import HeaderComponent from "@/Components/Header.vue";
import FooterComponent from "@/Components/Footer.vue"
import GuestLayout from "@/Layouts/Guest.vue"
import Wysiwyg from "@/Components/UI/Texts/Wysiwyg.vue"

export default {
  layout: GuestLayout,
  components: {
    HeaderComponent,
    FooterComponent,
    Heading,
    Head,
    Wysiwyg
  },
  data() {
    return {
      articles: [
        {
          title: "1 - Introdução",
          text: "Pellentesque habitant morbi tristique senectus. A lacus vestibulum sed arcu non odio euismod lacinia. Nisl nisi scelerisque eu ultrices vitae auctor eu. Quis risus sed vulputate odio ut enim blandit volutpat. Nec feugiat in fermentum posuere urna nec tincidunt. Id diam vel quam elementum. Elit ullamcorper dignissim cras tincidunt lobortis feugiat vivamus at augue. Amet cursus sit amet dictum sit amet justo donec enim. Ac ut consequat semper viverra. Dictumst vestibulum rhoncus est pellentesque elit ullamcorper. Euismod in pellentesque massa placerat"
        },
        {
          title: "2 - Dados Pessoais",
          text: "Pellentesque habitant morbi tristique senectus. A lacus vestibulum sed arcu non odio euismod lacinia. Nisl nisi scelerisque eu ultrices vitae auctor eu. Quis risus sed vulputate odio ut enim blandit volutpat. Nec feugiat in fermentum posuere urna nec tincidunt. Id diam vel quam elementum. Elit ullamcorper dignissim cras tincidunt lobortis feugiat vivamus at augue. Amet cursus sit amet dictum sit amet justo donec enim. Ac ut consequat semper viverra. Dictumst vestibulum rhoncus est pellentesque elit ullamcorper. Euismod in pellentesque massa placerat"
        }
      ]
    }
  }
  
}
</script>