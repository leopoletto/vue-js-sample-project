<template>
  <Head title="Seja Bem Vindo" />

  <section class="grid min-h-screen xl:grid-cols-0">
    <article class="component-background sm:hidden"></article>

    <article
      class="
        component-background-mobile
        grid
        xl:bg-white
        xl:justify-items-center
        xl:content-around
        sm:content-between
      "
    >
      <figure
        class="
          sm:grid
          sm:content-center
          sm:justify-center 
          sm:justify-items-center
          sm:pt-9
        "
      >
        <ApplicationLogo />
      </figure>
  
      <div
        class="sm:bg-white sm:grid sm:justify-items-stretch sm:content-around sm:py-6 sm:px-6 sm:rounded-md sm:mr-7 sm:ml-7 sm:mb-7"
      >
        <p class="text-black font-medium text-md text-center xl:pb-16 sm:hidden">
          Uma frase de efeito de duas <br />
          linhas na parte de cima da tela
        </p>

        <ul class="grid gap-4 xl:pb-32">
          <li>
            <Link
              :href="route('login')"
              class="
                text-md
                grid              
                font-semibold
                text-primary text-center
                p-1
                border-primary border rounded    
                mb-2          
              "
            >
              Acessar a Plataforma
            </Link>
          </li>

          <li>
            <Link
              :href="route('register')"
              class="
                text-md
                grid              
                font-semibold
                text-primary text-center
                p-1
                border-primary border rounded
              "
            >
              Criar Conta
            </Link>
          </li>
        </ul>

        <ul
          class="
            grid grid-cols-2
            justify-items-center
            xl:content-center
            xl:justify-center 
            xl:mt-12
            sm:mt-5
          "
        >
        <li>
            <Link :href="route('login')" class="text-xs text-gray-600">
              Acesse a plataforma
            </Link>
          </li>
          <li>
            <Link :href="route('register')" class="text-xs text-gray-600">
              Crie uma conta
            </Link>
          </li>
          <li>
            <Link :href="route('terms')" class="text-xs text-gray-600">
              Termos de Uso
            </Link>
          </li>
                  <li>
            <Link :href="route('faq')" class="text-xs text-gray-600">
              Perguntas Frequentes
            </Link>
          </li>      

          <li>
            <Link :href="route('fale-conosco')" class="text-xs text-gray-600">
              Fale Conosco
            </Link>
          </li>
        </ul>
      </div>
    </article>
  </section>
</template>

<script>
import { Head, Link } from "@inertiajs/inertia-vue3";
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
import Article from "@/Components/Article.vue";

export default {
  components: {
    Head,
    ApplicationLogo,
    Link,
    Article,
  },

  props: {
    canResetPassword: Boolean,
    canRegister: Boolean,
    status: String,
  },
};
</script>
