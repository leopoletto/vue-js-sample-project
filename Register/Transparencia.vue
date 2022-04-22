<template>
  <Head title="Transparência" />

  <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
    <div class="component-background sm:hidden"></div>

    <article>
      <header-component />
      <div class="sm:px-5 xl:px-28">
        <h2 class="text-3xl font-semibold text-primary text-left xl:py-6 sm:py-4">Transparência</h2>
        <p class="pb-2">Confira os Termos de Uso e Política de Privacidade da empresa</p>

        <form @submit.prevent="submit">
          <ul class="grid gap-5 pt-4">
            <li class="py-6 px-4 bg-gray-100">
              Pellentesque habitant morbi tristique senectus. A Iacus vestibulum
              sed arcu non odio euismod lacinia. Nisl nisi scelerisque eu
              ultrices vitae auctor eu. Quis risus sed vulputate odio ut enim
              blandit volutpat. Nec feugiat in fermentum posuere urna nec
              tincidunt. Id diam vel quam elementum. Elit ullamcorper dignissim
              cras tincidunt lobortis feugiat vivamus at augue. Amet cursus sit
              amet dictum sit amet justo donec enim. Ac ut consequat semper
              viverra. Dictumst vestibulum rhoncus est pellentesque elit
              ullamcorper. Euismod in pellentesque massa placerat duis ultricies
              Iacus. Dictum varius duis at consectetur lorem donec massa sapien,
              Nec tincidunt praesent semper feugiat nibh sed. Non tellus orci ac
              auctor augue mauris augue neque. Id diam maecenas ultricies mi
              eget mauris pharetra et ultrices. Suspendisse potenti nullam ac
              tortor. Neque vitae tempus quam pellentesque
            </li>
            <div class="flex">
              <input class="hover:bg-gray-600 self-start mt-1 mr-2" type="checkbox" id="acceptFirstTerms" name="acceptFirstTerms" value="acceptFirstTerms" v-model="acceptFirstTerms">
              <label for="acceptTerms"> Autorizo o envio de comunicações, como e-mails, sms e formulários de pesquisa.</label>
            </div>
            <div class="flex">
              <input class="hover:bg-gray-600 self-start mt-1 mr-2" type="checkbox" id="acceptSecondTerms" name="acceptSecondTerms" value="acceptSecondTerms" v-model="acceptSecondTerms">
              <label for="acceptTerms"> Li e concordo com os termos de uso.</label>
            </div>

            <li>
              <Button
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
              </Button>
            </li>
            <ul
              class="
                grid grid-cols-2
                justify-items-center
                xl:content-center
                xl:justify-center 
                xl:mt-5
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
    <ValidationErrors :errors="errors" />
  </section>
</template>

<script>
import HeaderComponent from "@/Components/Header.vue";
import Input from "@/Components/UI/Form/Input.vue";
import Select from "@/Components/Select.vue"

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
    Select
  },

  props: {
    acceptEnvioDeComunicacoes: Boolean,
    acceptTermosDeTransparencia: Boolean
  },

  data() {
    return {
      form: this.$inertia.form({
        cpf: sessionStorage.getItem("cpf"),
        name: sessionStorage.getItem("nome"),
        email: sessionStorage.getItem("email"),
        password: sessionStorage.getItem("senha"),
        dataDeNascimento: sessionStorage.getItem("data"),
        username: sessionStorage.getItem("nomeDeUsuario"),
        nickname: sessionStorage.getItem("nickname"),
      }),
      errors: []
      //inputClasses:
      //"overflow-visible py-1 px-3 m-0 w-full h-12 text-xs font-normal text-white bg-clip-padding bg-transparent rounded-none border-b border-white border-solid box-border outline-none mt-1 block w-full",
    };
  },

  methods: {
    submit() {
      this.errors = [];
      if(this.acceptSecondTerms) {
        sessionStorage.setItem('acceptEnvioDeComunicacoes', this.acceptEnvioDeComunicacoes)
        sessionStorage.setItem('acceptTermosDeTransparencia', 'true')

        this.$inertia.post("/register/apelido", this.form);
      } else {
        this.errors.push('Aceite os termos para prosseguirmos')
      }
      // this.form.post(this.route("register"), {
      //   onFinish: () => this.form.reset("password", "password_confirmation"),
      // });
    },
    formatCpf,
  },
};
</script>