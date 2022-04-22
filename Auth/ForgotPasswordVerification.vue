<template>
    <Head title="Forgot Password" />
    <Header />

    <div class="px-5">
        <button class="text-xs text-indigo-500 mt-4">botão de voltar aqui</button>
        <h2 class="text-3xl font-semibold text-primary xl:px-24 pb-6">Código de verificação</h2>
        <p class="text-xl">Nós enviamos o código de verificação para o email:</p>
        <span class="text-xl font-bold pt-2 pb-6 inline-block">{{ recoveryEmail }}</span>
        

        <form @submit.prevent="submit" class="mb-6">
          <ul class="grid gap-5 pt-6">
            <li class="mb-14">
              <label class="mb-1 mr-5 flex font-bold pb-1">Insira o Código</label>
              <Input
                placeholder="*********"
                v-model="form.code"
                type="text"
                required
                autofocus
              />
            </li>

            <li>
              <button
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
                Verificar Código
              </button>
            </li>
          </ul>
        </form>
        <button
            @click.prevent="showModal = true"
            class="
                w-full
                grid
                justify-items-center
                items-center
                text-primary
                font-semibold
                p-3.5
                border-[1px]
                rounded-sm
                border-primary
            "
            >
            Reenviar o Código
        </button>
    </div>
    <div v-if="$page.props.flash.error">
      {{ $page.props.flash.error }}
    </div>
    <div v-if="$page.props.flash.success">
        {{ $page.props.flash.success }}
    </div>
    <transition>
      <div v-if="showModal" class="fixed right-0 left-0 top-0 bottom-0 z-[99] bg-[#707070] bg-opacity-70 flex justify-center items-center">
        <div class="bg-white border-[1px] border-primary rounded-[4px] mx-2.5 w-full pl-4 pr-2 pt-2 pb-2 leading-9">
          <button class="float-right" @click="showModal = false">
            <Icon name="Fechar"/>
          </button>
          <h1 class="text-[20px] font-bold text-primary">Código Enviado</h1>
          <p class="text-[16px] leading-6">O código de verificação foi enviado para o seu email.</p>
        </div>
      </div>
    </transition>
</template>
<script>
import Input from "@/Components/UI/Form/Input.vue";
import Icon from '@/Components/UI/Icons/Icon.vue'

import Header from '@/Components/UI/Nav/Header.vue'
import { Head } from "@inertiajs/inertia-vue3";

export default {
    components: {
        Header,
        Head,
        Input,
        Icon
    },
    props: {
      status: String,
    },
    data() {
        return {
          recoveryEmail: sessionStorage.getItem('recoveryEmail'),
          showModal: true,
          form: this.$inertia.form({
              code: "",
              email: sessionStorage.getItem('recoveryEmail'),
          })
        }
    },
    methods: {
      submit() {
        
        if(this.form) {
          sessionStorage.setItem('code', this.form.code)
          this.$inertia.post('/forgot-password-verification', this.form);
        }
      }
    }
}
</script>