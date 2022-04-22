<template>
    <Head title="Meus dados" />

    <AuthenticatedLayout>
        
        <section class="w-full">

            <form class="w-[500px] sm:w-full sm:overflow-visible sm:h-auto mx-auto h-[calc(100vh-121px)] overflow-y-scroll px-5">
                <fieldset class="w-full">
                    <h2 class="mb-4 text-white text-[15px] font-bold uppercase">Dados pessoais</h2>

                    <div class="flex gap-7">
                        <Field label="CPF" required labelFor="cpf" class="w-1/2">
                            <Input @keyup="formatCpf" v-model="form.cpf" :class="inputClasses" id="cpf" type="text" />
                        </Field>
                        <Field label="Data de nascimento" required labelFor="birthdate" class="w-1/2">
                            <Input  @keyup="formatDate" v-model="form.birthdate" :class="inputClasses" id="birthdate" type="text" />
                        </Field>
                    </div>
                    <div class="flex mt-2">
                        <Field label="Nome" required labelFor="name" class="w-full">
                            <Input v-model="form.name" disabled :class="inputClasses" id="name" type="text" />
                        </Field>
                    </div>
                    <div class="flex mt-2">
                        <Field label="Distribuidora" required labelFor="distributor" class="w-full">
                            <Input v-model="form.distributor" disabled :class="inputClasses" id="distributor" type="text" />
                        </Field>
                    </div>
                    <div class="flex mt-2">
                        <Field label="Cargo" required labelFor="role" class="w-full">
                            <Input v-model="form.role" disabled :class="inputClasses" id="role" type="text" />
                        </Field>
                    </div>
                    <div class="flex mt-2">
                        <Field label="Instagram" labelFor="instagram" class="w-full">
                            <Input v-model="form.instagram" :class="inputClasses" id="instagram" type="text" />
                        </Field>
                    </div>
                    <div class="flex mt-2 gap-7">
                        <Field label="Sexo" labelFor="gender" class="w-2/5">
                            <Select placeholder="Selecione" :options="genderOptions" v-model="form.gender" :class="inputClasses" id="gender" />
                        </Field>
                        <Field label="Filhos" labelFor="children" class="w-1/5">
                            <Input v-model="form.children" :class="inputClasses" id="children" type="number" />
                        </Field>
                        <Field label="Estado civil" labelFor="civil-status" class="w-2/5">
                            <Select placeholder="Selecione" :options="civilStatusOptions" v-model="form.civilStatus" :class="inputClasses" id="civil-status" />
                        </Field>
                    </div>
                </fieldset>

                <fieldset class="w-full mt-8">
                    <h2 class="mb-4 text-white text-[15px] font-bold uppercase">Contato</h2>

                    <div class="flex gap-7">
                        <Field label="Telefone comercial" required labelFor="phone" class="w-1/2">
                            <Input @keyup="formatPhoneNumber" v-model="form.phone" :class="inputClasses" id="phone" type="text" />
                        </Field>
                        <Field label="Telefone celular" required labelFor="cellphone" class="w-1/2">
                            <Input @keyup="formatPhoneNumber" v-model="form.cellphone" :class="inputClasses" id="cellphone" type="text" />
                        </Field>
                    </div>
                    <div class="flex mt-2 gap-7">
                        <Field label="E-mail" required labelFor="email" class="w-1/2">
                            <Input v-model="form.email" :class="inputClasses" id="email" type="email" />
                        </Field>
                        <Field label="Confirmar e-mail" required labelFor="email-confirmation" class="w-1/2">
                            <Input v-model="form.emailConfirmation" :class="inputClasses" id="cellphone" type="email-confirmation" />
                        </Field>
                    </div>
                </fieldset>

                <fieldset class="w-full mt-8">
                    <h2 class="mb-4 text-white font-bold uppercase">Endereço</h2>

                    <div class="flex gap-7">
                        <Field label="CEP" required labelFor="postal-code" class="w-3/5">
                            <Input @keyup="formatPostalCode" v-model="form.postalCode" :class="inputClasses" id="postal-code" type="text" />
                        </Field>
                        <div class="w-2/5 content-end self-end pb-1.5">
                            <a href="#" class="uppercase text-xs hover:text-blue-600 text-white underline font-bold">Não sei meu cep</a>
                        </div>
                    </div>

                    <div class="flex mt-2 gap-7">
                        <Field label="Endereço" required labelFor="address" class="w-4/6">
                            <Input v-model="form.address" :class="inputClasses" id="address" type="text" />
                        </Field>
                        <Field label="Número" required labelFor="number" class="w-2/6">
                            <Input v-model="form.number" :class="inputClasses" id="number" type="text" />
                        </Field>
                    </div>

                    <div class="flex mt-2 gap-7">
                        <Field label="Complemento" labelFor="complement" class="w-2/6">
                            <Input v-model="form.complement" :class="inputClasses" id="complement" type="text" />
                        </Field>
                        <Field label="Bairro" required labelFor="district" class="w-4/6">
                            <Input v-model="form.district" :class="inputClasses" id="district" type="text" />
                        </Field>
                    </div>

                    <div class="flex mt-2 gap-7">
                        <Field label="Cidade" labelFor="city" class="w-1/2">
                            <Input v-model="form.city" :class="inputClasses" id="city" type="text" />
                        </Field>
                        <Field label="Estado" required labelFor="state" class="w-1/2">
                            <Select placeholder="Selecione" :options="stateOptions" v-model="form.state" :class="inputClasses" id="state" />
                        </Field>
                    </div>
                </fieldset>

                <fieldset class="w-full mt-8">
                    <h2 class="mb-4 text-white font-bold text-[15px] uppercase">Senha</h2>

                    <p class="mb-4 text-white text-sm">Preencha somente se você deseja alterar sua senha.</p>

                    <div class="flex">
                        <Field label="Escolha uma senha" required labelFor="name" class="w-full">
                            <Input v-model="form.password" :class="inputClasses" id="name" type="password" />
                        </Field>
                    </div>
                    <div class="flex mt-2">
                        <Field label="Confirme a senha" required labelFor="password-confirmation" class="w-full">
                            <Input v-model="form.passwordConfirmation" :class="inputClasses" id="password-confirmation" type="password" />
                        </Field>
                    </div>
                </fieldset>

                <Button class="w-full !text-sm uppercase my-5" type="submit">Salvar dados e continuar</Button>
            </form>

        </section>
    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from '@/Layouts/Authenticated.vue'
import Input from '@/Components/Input.vue'
import Select from '@/Components/Select.vue'
import Field from '@/Components/Field.vue'
import Button from '@/Components/Button.vue'
import { Head } from '@inertiajs/inertia-vue3';
import { formatCpf, formatDate, formatPhoneNumber, formatPostalCode} from '@/Helpers/masks';

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Input,
        Select,
        Button,
        Field,
    },
    methods: {
        formatCpf,
        formatDate,
        formatPhoneNumber,
        formatPostalCode,
    },
    props:{
        profileData: {
            type: Object,
            default: {}
        },
        stateOptions: {
            type: Object,
            default: {}
        },
        genderOptions: {
            type: Object,
            default: {}
        },
        civilStatusOptions: {
            type: Object,
            default: {}
        }
    },
    data(){
        return {
            form: this.$inertia.form(this.profileData),
            inputClasses: 'text-xs disabled:opacity-60 text-pink-900 bg-white rounded-3xl border-none px-3 py-2 leading-relaxed outline-none w-full',
        }
    }
}
</script>
