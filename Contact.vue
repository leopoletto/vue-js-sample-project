<template>
    <Head title="Fale Conosco" />

    <AuthenticatedLayout>
        
        <section class="w-full mx-auto px-5">
            <form>
                <fieldset class="w-full">
                    <h2 class="mb-4 text-white text-center text-[28px] font-bold">Fale Conosco</h2>

                    <p class="mb-4 text-white text-sm leading-relaxed">
                        Olá, <strong>{{ auth.user.name }}</strong>! Neste espaço, você pode nos enviar elogios, sugestões de melhoria e também reclamações. 
                        Entraremos em contato com você pelos seus dados de cadastro, por isso, é importante que você atualize seu cadastro 
                        antes de enviar a mensagem, combinado?
                    </p>

                    <div class="flex mt-2">
                        <Field label="Nome" labelFor="name" class="w-full">
                            <Input v-model="form.name" disabled :class="inputClasses" id="name" type="text" />
                        </Field>
                    </div>

                    <div class="flex mt-2">
                        <Field label="E-mail" labelFor="email" class="w-full">
                            <Input v-model="form.email" disabled :class="inputClasses" id="email" type="email" />
                        </Field>
                    </div>

                    <div class="flex mt-2">
                        <Field label="WhatsApp" labelFor="phone" class="w-full">
                            <Input @keyup="formatPhoneNumber" v-model="form.phone" :class="inputClasses" id="phone" type="text" />
                        </Field>
                    </div>

                    <p class="mt-8 mb-4">
                        <Link class="text-white text-xs font-bold underline" :href="route('profile')">Editar meus dados</Link>
                    </p>

                    <div class="flex mt-2">
                        <Field label="Assunto" required labelFor="subject" class="w-full">
                            <Input v-model="form.subject" :class="inputClasses" id="subject" type="text" />
                        </Field>
                    </div>

                    <div class="flex mt-2">
                        <Field label="Mensagem" required labelFor="message" class="w-full">
                            <Textarea rows="2" v-model="form.message" :class="inputClasses" id="message"/>
                        </Field>
                    </div>


                </fieldset>

                <Button class="w-full !text-sm uppercase my-5" type="submit">Enviar</Button>
            </form>
        </section>
        

    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from '@/Layouts/Authenticated.vue'
import Input from '@/Components/Input.vue'
import Textarea from '@/Components/Textarea.vue'
import Field from '@/Components/Field.vue'
import Button from '@/Components/Button.vue'
import { Head, Link } from '@inertiajs/inertia-vue3';
import { formatPhoneNumber } from '@/Helpers/masks';

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Input,
        Textarea,
        Button,
        Field,
        Link,
    },
    methods: {
        formatPhoneNumber,
    },
    props:['auth'],
    data(){
        return {
            form: this.$inertia.form({
                name: 'John Doe',
                email: 'leonardo.poletto@digi.ag',
                phone: '(99) 9999-99999',
                subject: '',
                message: '',
            }),
            inputClasses: 'text-xs disabled:opacity-60 text-pink-900 bg-white rounded-3xl border-none px-3 py-2 leading-relaxed outline-none w-full',
        }
    }
}
</script>
