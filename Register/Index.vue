<template>
  <Head title="Register" />

  <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
    <div class="component-background sm:hidden"></div>

    <article>
      <header-component />
            
      <div class="sm:px-5 xl:px-28">
        <h2 class="text-3xl font-semibold text-primary text-left xl:py-6 sm:py-4">Faça Parte</h2>
        <p class="pb-2 ">
          Seja bem-vindo(a),
        </p>
        <p>
          Para começar, digite seu <strong>CPF</strong> abaixo:
        </p>

        <form @submit.prevent="submit">
          <ul class="grid gap-5 pt-4">
            <li>
              <label class="mb-1 mr-5 flex font-semibold"> CPF </label>
              <Input
                placeholder="000.000.000-00"
                @keyup="formatCpf"
                id="cpf"
                type="text"
                v-model="inputCpf"
                required
                :state="stateCpf"
                autocomplete="cpf"
              />
              <div v-if="$page.props.flash.error" class="flashError text-[10px] text-error">
                {{ $page.props.flash.error }}
              </div>
            </li>
            <li>
              <span class="text-xs pt-0 pb-4 flex">
                *O CPF informado deve ser completo, sem 
                separadores de números, pontos ou traços.
              </span>

              <button
                class="
                  w-full
                  grid
                  justify-items-center
                  items-center
                  text-primary
                  border-primary border rounded
                hover:bg-gray-500
                  hover:border-0
                  font-semibold
                  p-2
                "
              >
                Acessar
              </button>
            </li>
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
          </ul>
          
        </form>
      </div>

    </article>
  </section>
</template>

<script>
import HeaderComponent from "@/Components/Header.vue";
import Input from "@/Components/UI/Form/Input.vue";

import GuestLayout from "@/Layouts/Guest.vue";
import Label from "@/Components/Label.vue";
import ValidationErrors from "@/Components/ValidationErrors.vue";
import { Head, Link } from "@inertiajs/inertia-vue3";
import { formatCpf } from "@/Helpers/masks";

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

  data() {

    return {
      form: this.$inertia.form({
        name: "",
        email: "",
        cpf: "",
        password: "",
        password_confirmation: "",
        terms: false,
      }),
      stateCpf: '',
      inputCpf: ''
      
    };
  },

  methods: {
    submit() {
      const cpfNoFormat = this.inputCpf.replace('.', '').replace('.', '').replace('-', '');

      let cpfFormated = cpfNoFormat;

      cpfFormated = cpfFormated.replace(/\D/g, "")
      cpfFormated = cpfFormated.replace(/(\d{3})(\d)/, "$1.$2")
      cpfFormated = cpfFormated.replace(/(\d{3})(\d)/, "$1.$2")
      cpfFormated = cpfFormated.replace(/(\d{3})(\d{1,2})$/, "$1-$2")

      this.form.cpf = cpfFormated;

      if(cpfNoFormat.length > 10) {
        this.form.post(this.route("register"), {
          onFinish: () => this.form.reset("password", "password_confirmation"),
          onFinish: () => sessionStorage.setItem('cpf', this.form.cpf)
        });
      } else {
        this.stateCpf = 'error'
      }
    },
    formatCpf,
  },
};
</script>
