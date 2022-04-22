<template>
  <Head title="Register senha" />

  <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
    <div class="component-background sm:hidden"></div>

    <article>
      <header-component />
      <div class="sm:px-5 xl:px-28">
        <p class="pb-2">
          Como você gostaria de ser <br />
          chamado(a)? Esse será o nome que <br />
          aparecerá na tela de início.
        </p>

        <form @submit.prevent="submit">
          <ul class="grid gap-5 pt-4">
            <li>
              <label class="mb-1 mr-5 flex font-semibold pb-1">
                Apelido:
              </label>
              <Input
                placeholder="Preecha aqui o seu apelido.."
                type="text"
                required
                v-model="apelido"
              />
            </li>

            <li>
              <Button
                class="
                  bg-disabled
                  w-full
                  grid
                  justify-items-center
                  items-center
                  text-gray-700
                  font-semibold
                  p-3.5
                "
              >
                Avançar
              </Button>
            </li>
          </ul>
        </form>
      </div>
    </article>
  </section>
</template>

<script>
import HeaderComponent from "@/Components/Header.vue";
import Input from "@/Components/UI/Form/Input.vue";

//import Button from "@/Components/Button.vue";
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

  props: {
    apelido: String
  },

  data() {
    return {
      form: this.$inertia.form({
        cpf: sessionStorage.getItem('cpf'),
        name: sessionStorage.getItem('nome'),
        email: sessionStorage.getItem('email'),
        password: sessionStorage.getItem('senha'),
        dataDeNascimento: sessionStorage.getItem('data'),
        apelido: sessionStorage.getItem('apelido'),
      }),
      //inputClasses:
      //"overflow-visible py-1 px-3 m-0 w-full h-12 text-xs font-normal text-white bg-clip-padding bg-transparent rounded-none border-b border-white border-solid box-border outline-none mt-1 block w-full",
    };
  },

  methods: {
    submit() {
      this.form.apelido = this.apelido;
      this.$inertia.post('/register-apelido', this.form);
      // location.href = "/register-regulamento";
      // this.form.post(this.route("register"), {
      //   onFinish: () => this.form.reset("password", "password_confirmation"),
      // });
      // location.href = "/register-regulamento";
      // this.form.post(this.route("register"), {
      //   onFinish: () => this.form.reset("password", "password_confirmation"),
      // });
    },
    formatCpf,
  },
};
</script>
