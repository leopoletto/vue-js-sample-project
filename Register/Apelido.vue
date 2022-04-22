<template>
    <Head title="Register Apelido" />

    <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
        <div class="component-background sm:hidden"></div>

        <article>
            <header-component />
            <div class="sm:px-5 xl:px-28">
                <h2 class="text-3xl font-semibold text-primary text-left xl:py-6 sm:py-4">Apelido</h2>
                <p class="pb-2">
                    Como você gostaria de ser
                    chamado(a)? Esse será o nome que 
                    aparecerá na tela de início.
                </p>

                <form @submit.prevent="submit">
                    <ul class="grid gap-5 pt-4">
                        <li>
                            <label class="mb-1 mr-5 flex font-semibold">
                                Apelido
                            </label>
                            <Input
                                placeholder="Preecha aqui o seu apelido.."
                                type="text"
                                required
                                v-model="form.nickname"
                            />
                        </li>

                        <li>
                            <Button
                                class="
                                    w-full
                                    grid
                                    justify-items-center
                                    items-center
                                  text-primary
                                  hover:bg-gray-300
                                  border-primary border rounded
                                    hover:border-0
                                    font-semibold
                                    p-1.5
                                "
                            >
                                Avançar
                            </Button>
                        </li>
                    </ul>
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
        apelido: String,
    },

    data() {
        return {
            form: this.$inertia.form({
                cpf: sessionStorage.getItem("cpf"),
                name: sessionStorage.getItem("nome"),
                email: sessionStorage.getItem("email"),
                password: sessionStorage.getItem("senha"),
                dataDeNascimento: sessionStorage.getItem("data"),
                nickname: '',
            }),
            //inputClasses:
            //"overflow-visible py-1 px-3 m-0 w-full h-12 text-xs font-normal text-white bg-clip-padding bg-transparent rounded-none border-b border-white border-solid box-border outline-none mt-1 block w-full",
        };
    },

    methods: {
        submit() {
            console.log(this.form);
            if(this.form.nickname) {
                sessionStorage.setItem('nickname', this.form.nickname)
                location.href = "/register/regulamento";
            }
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
