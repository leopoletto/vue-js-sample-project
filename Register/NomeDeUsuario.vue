<template>
    <Head title="Register Nome de Usuário" />

    <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
        <div class="component-background sm:hidden"></div>

        <article>
            <header-component />
            <div class="sm:px-5 xl:px-28">
                <h2 class="text-3xl font-semibold text-primary text-left xl:py-6 sm:py-4">Nome de Usuário</h2>
                <p class="pb-2">
                    Qual o nome de usuário <br />
                    que você gostaria de usar 
                    para logar?
                </p>

                <form @submit.prevent="submit">
                    <ul class="grid gap-5 pt-4">
                        <li>
                            <label class="mb-1 mr-5 flex font-semibold pb-1">
                                Nome de Usuário
                            </label>
                            <Input
                                placeholder="Preecha aqui o seu nome de usuário.."
                                type="text"
                                required
                                v-model="form.nomeDeUsuario"
                            />
                        </li>

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
                nomeDeUsuario: '',
            }),
        };
    },

    methods: {
        submit() {
            console.log(this.form);
            sessionStorage.setItem('nomeDeUsuario', this.form.nomeDeUsuario);
            location.href = '/register/senha';
        },
    },
};
</script>
