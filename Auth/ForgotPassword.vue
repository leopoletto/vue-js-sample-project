<template>
  <Head title="Forgot Password" />
  <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
    <div class="component-background sm:hidden"></div>

    <article>
      <header-component />

      <div class="sm:px-5 xl:px-28">
        <p class="pb-2 text-sm">
          Para recuperar a senha, precisamos verificar se é você mesmo.
        </p>

        <p class="text-sm">
          Digite seu email cadastrado e nós enviaremos um código de verificação.
        </p>

        <form @submit.prevent="submit">
          <ul class="grid gap-5 pt-4">
            <li>
              <label class="mb-1 mr-5 flex font-semibold pb-1"> Email </label>
              <Input
                placeholder="Exemplo: joao@email.com"
                id="email"
                type="email"
                v-model="form.email"
                required
                autofocus
                autocomplete="username"
              />
            </li>

            <li>
              <button
                class="
                  sm:bg-disabled
                  xl:border-primary border-2 rounded
                  w-full
                  grid
                  justify-items-center
                  items-center
                  text-primary
                  font-semibold
                  p-0.5
                "
              >
                Enviar Código
              </button>

            </li>
          </ul>
        </form>
        
      </div>
      <ul
          class="
            grid grid-cols-2
            justify-items-center
            xl:content-center
            xl:justify-center 
            xl:mt-5
            xl:py-10
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
    </article>
  </section>
            <div v-if="$page.props.flash.error">
                {{ $page.props.flash.error }}
            </div>

            <div v-if="$page.props.flash.success">
                {{ $page.props.flash.success }}
            </div>
</template>

<script>
import HeaderComponent from "@/Components/Header.vue";
import Input from "@/Components/UI/Form/Input.vue";

import GuestLayout from "@/Layouts/Guest.vue";
import Label from "@/Components/Label.vue";
import ValidationErrors from "@/Components/ValidationErrors.vue";
import { Head } from "@inertiajs/inertia-vue3";

export default {
  layout: GuestLayout,

  components: {
    HeaderComponent,
    Input,
    Label,
    ValidationErrors,
    Head,
  },

  props: {
    status: String,
  },

  data() {
    return {
      form: this.$inertia.form({
        email: "",
      }),
      inputClasses:
        "overflow-visible py-1 px-3 m-0 w-full h-12 text-xs font-normal text-white bg-clip-padding bg-transparent rounded-none border-b border-white border-solid box-border outline-none mt-1 block w-full",
    };
  },

  methods: {
    submit() {
      if(this.form.email) {

        this.$inertia.post('/forgot-password', this.form);
        sessionStorage.setItem('recoveryEmail', this.form.email);
      }
      // this.form.post(this.route("password.email"));
    },
  },
};
</script>
