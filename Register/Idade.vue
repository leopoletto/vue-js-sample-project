<template>
  <Head title="Register Idade" />

  <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
    <div class="component-background sm:hidden"></div>

    <article>
      <header-component />
      <div class="sm:px-5 xl:px-28">
        <h2 class="text-3xl font-semibold text-primary text-left xl:py-6 sm:py-4">Data de Nascimento</h2>
        <p class="pb-2">
          Insira a <strong> data de nascimento </strong> de 
          acordo com os seus documentos.
        </p>

        <form @submit.prevent="submit">
          <ul class="grid gap-5 pt-4 pb-12 grid-flow-col">
            <li>
              <label class="mb-1 mr-5 flex font-semibold"> Dia </label>
              <Input @keyup="onlyNumbers" maxlength="2" v-model="dia" placeholder="DD" type="text" :state="stateDia" required />
            </li>

            <li>
              <label class="mb-1 mr-5 flex font-semibold"> Mês </label>
              <Input @keyup="onlyNumbers" maxlength="2" v-model="mes" placeholder="MM" type="text" :state="stateMes" required />
            </li>

            <li>
              <label class="mb-1 mr-5 flex font-semibold"> Ano </label>
              <Input @keyup="onlyNumbers" maxlength="4" v-model="ano" placeholder="AAAA" type="text" :state="stateAno" required />
            </li>
          </ul>

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
              sm:my-0
            "
          >
            Avançar
          </button>
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
        </form>
      </div>
    </article>
    <ValidationErrors :errors="errors" />
  </section>
</template>

<script>
import HeaderComponent from "@/Components/Header.vue";
import Input from "@/Components/UI/Form/Input.vue";

import GuestLayout from "@/Layouts/Guest.vue";
import Label from "@/Components/Label.vue";
import ValidationErrors from "@/Components/ValidationErrors.vue";
import { onlyNumbers } from "@/Helpers/masks";
import { Head, Link } from "@inertiajs/inertia-vue3";

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
    dia: Number,
    mes: Number,
    ano: Number
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
      errors: [],
      stateDia: '',
      stateMes: '',
      stateAno: ''
      //inputClasses:
      //"overflow-visible py-1 px-3 m-0 w-full h-12 text-xs font-normal text-white bg-clip-padding bg-transparent rounded-none border-b border-white border-solid box-border outline-none mt-1 block w-full",
    };
  },

  methods: {
    submit() {
      const dataAtual = new Date();
      this.errors = [];
      this.stateDia = "success";
      this.stateMes = "success";
      this.stateAno = "success";

      if(this.dia < 1 || this.dia > 31){
        this.stateDia = "error"
        this.errors.push('O dia é inválido')
      }
      if(this.mes < 1 || this.mes > 12){
        this.stateMes = "error"
        this.errors.push('O mês é inválido')
      } 
      if(this.ano < 1900 || this.ano > dataAtual.getFullYear() ){
        this.stateAno = "error"
        this.errors.push('O ano é inválido')
      } 
      if(dataAtual.getFullYear() - this.ano < 18 ) {
        this.stateAno = "error"
        this.errors.push('Você precisa ter mais de 18 anos')
      }
      if(dataAtual.getFullYear() - this.ano == 18) {
        if(this.mes > dataAtual.getMonth()+1) {
          this.stateAno = "error"
          this.errors.push('Você precisa ter mais de 18 anos')
        } else {
          if(this.mes == dataAtual.getMonth()+1) {
            if(this.dia > dataAtual.getDate()) {
              this.stateAno = "error"
              this.errors.push('Você precisa ter mais de 18 anos')
            }
          }
        }
      }
      if(this.errors.length === 0) {
        sessionStorage.setItem('data', this.dia+"/"+this.mes+"/"+this.ano);
        location.href = "/register/primeiro-nome";
      }
    },
    onlyNumbers
  },
};
</script>
