<template>
    <Head title="Log in" />

    <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
        <div class="component-background sm:hidden"></div>

        <article class="grid">
            <Header-component />

            <form @submit.prevent="submit" class="sm:px-5 xl:px-28" novalidate>
                <ul class="grid gap-5">
                    <li>
                        <label class="mb-1 mr-5 flex font-semibold">
                            Nome do usuário
                        </label>
                        <Input
                            type="text"
                            placeholder="Exemplo: Beto"
                            v-model="form.cpf"
                        />
                    </li>

                    <li>
                        <label class="mb-1 mr-5 flex font-semibold">
                            Senha
                        </label>
                        <Input
                            ref="inputPassword"
                            id="password"
                            name="password"
                            type="password"
                            placeholder="******"
                            v-model="form.password"
                            required
                            autocomplete="current-password"
                        />

                        <Link
                            ref="passwordRequest"
                            :href="route('password.request')"
                            class="
                                my-2
                                pt-2
                                hover:underline
                                text-xs
                                table
                                float-right
                                justify-items-end
                                hover:text-blue-600
                            "
                        >
                            Esqueceu a senha?
                        </Link>
                    </li>

                    <li>
                        <button
                            class="
                                w-full
                                grid
                                justify-items-center
                                items-center
                                text-primary text-center
                                p-2
                                text-md          
                              border-primary border rounded
                              hover:border-0
                              hover:bg-gray-300
                            "
                        >
                            Acessar
                        </button>
                        <div v-if="$page.props.flash.error">
                            {{ $page.props.flash.error }}
                        </div>
                    </li>
                </ul>
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
            </form>
        </article>
    </section>
</template>

<script>
import HeaderComponent from "@/Components/Header.vue";
import Input from "@/Components/UI/Form/Input.vue";

//import Button from "@/Components/Button.vue";
import Checkbox from "@/Components/Checkbox.vue";
import GuestLayout from "@/Layouts/Guest.vue";
import Label from "@/Components/Label.vue";
import ValidationErrors from "@/Components/ValidationErrors.vue";
import { Head, Link } from "@inertiajs/inertia-vue3";
import { formatCpf } from "@/Helpers/masks";

//import Input from '@/Components/Input.vue'

import { reactive } from "vue";
import { Inertia } from "@inertiajs/inertia";

export default {
    layout: GuestLayout,

    components: {
        HeaderComponent,
        //Button,
        Checkbox,
        Input,
        Label,
        ValidationErrors,
        Head,
        Link,
    },

    props: {
        canResetPassword: Boolean,
        canRegister: Boolean,
        status: String,
    },

    data() {
        return {
            form: {
                cpf: "",
                password: "",
            },
            //inputClasses: "overflow-visible py-1 px-3 m-0 w-full h-12 text-xs font-normal text-white bg-clip-padding bg-transparent rounded-none border-b border-white border-solid box-border outline-none mt-1 block w-full",
        };
    },

    methods: {
        onChange(e) {
            console.log(e);
        },
        submit() {
            //   if (this.form.password === "") {
            //     this.$refs.inputPassword.$el.classList.remove("invisible");
            //     this.$refs.inputPassword.focus();
            //     this.$refs.passwordRequest.$el.classList.remove("invisible");
            //     return false;
            //   }
            this.$inertia.post(this.route("login"), this.form);
            // this.form.post(this.route("login"), {
            //     onFinish: () => this.form.reset("password"),
            // });

            console.log(this.form);
        },
        formatCpf,
    },
};
</script>
