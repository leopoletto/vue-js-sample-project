<template>
  <Head title="Regulamento" />

  <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
    <div class="component-background sm:hidden"></div>

    <article>
      <header-component />
      <div class="sm:px-5 xl:px-28">
        <h2 class="text-3xl font-semibold text-primary text-left xl:py-6 sm:py-4">Regulamento</h2>
        <p class="pb-2">Saiba mais sobre as regras da campanha:</p>

        <form @submit.prevent="submit">
          <ul class="grid gap-5 pt-4">
            <li class="py-6 px-4 bg-gray-100" v-html="regulation.text"></li>
            <div class="flex" v-for="(regulationAccept, index) in regulation.regulationAccepts" :key="index">
              <input class="hover:bg-gray-600 self-start mt-1 mr-2" type="checkbox" :id="'acceptTerms-' + index " :name="'acceptTerms-' + index " :value="regulationAccept.id" v-model="acceptTerms[regulationAccept.id]">
              <label  :for="'acceptTerms-' + index ">{{ regulationAccept.text }}</label>
            </div>

            <li>
              <button
                class="
                  w-full
                  grid
                  justify-items-center
                  items-center
                text-primary
                border-primary border rounded
                hover:bg-gray-300
                  hover:border-0
                  font-semibold
                  p-1.5
                "
              >
                Avançar
              </button>
            </li>
            <ul
              class="
                grid grid-cols-2
                justify-items-center
                xl:content-center
                xl:justify-center 
                xl:mt-12
                sm:mt-8
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
          </ul>
        </form>
      </div>
    </article>
    <ValidationErrors :errors="errors" />
  </section>
</template>

<script>
import GuestLayout from "@/Layouts/Guest.vue";
import HeaderComponent from "@/Components/Header.vue";
import Input from "@/Components/UI/Form/Input.vue";
import Label from "@/Components/Label.vue";
import ValidationErrors from "@/Components/ValidationErrors.vue";
import { Head, Link } from "@inertiajs/inertia-vue3";
import { Inertia } from '@inertiajs/inertia'

export default {
  layout: GuestLayout,

  components: {
    HeaderComponent,
    Input,
    Label,
    ValidationErrors,
    Head,
    Link,
  },

  props: {
    regulation: Object,
    acceptTerms: {
      type: Object,
      default: {}
    },
  },

  data() {
    return {
      errors: [],    
    };
  },

  methods: {
    submit() {
      this.errors = [];

      const terms = JSON.parse(
        JSON.stringify(this.acceptTerms)
      );

      if(Object.values(terms).filter(accepted => !accepted).length === 0) {
        sessionStorage.setItem('acceptRegulamento', JSON.stringify(terms))
        Inertia.visit('/register/transparencia', { method: 'get' })
      } else {
        this.errors.push('Aceite o regulamento para prosseguirmos')
      }
    },
  },
};
</script>
