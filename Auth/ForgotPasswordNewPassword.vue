<template>
    <Head title="Forgot Password" />
    <Header />

    <div class="px-5">
        <button class="text-xs text-indigo-500 mt-4">botão de voltar aqui</button>
        <h2 class="text-3xl font-semibold text-primary xl:px-24 pb-6">Nova Senha</h2>
        <p class="text-xl pb-4">Crie uma <strong>senha</strong> forte que só você saiba. Ela precisa ter:</p>
        
        <ul>
          <li class="flex items-center pb-1">
            <Icon :name="isValid(hasEightChar)"/>
            <p class="ml-2.5">Mínimo de 8 caracteres</p>
          </li>
          <li class="flex items-center pb-1">
            <Icon :name="isValid(hasUpperCase)" />
            <p class="ml-2.5">Um caractere maiúsculo</p>
          </li>
          <li class="flex items-center pb-1">
            <Icon :name="isValid(hasLowerCase)" />
            <p nome="isValid" class="ml-2.5">Um caractere minúsculo</p>
          </li>
          <li class="flex items-center">
            <Icon :name="isValid(hasNumber)" />
            <p class="ml-2.5">Um número</p>
          </li>
        </ul>
        

        <form @submit.prevent="submit" class="mb-6">
          <ul class="pt-6">
            <li class="mb-4">
              <label class="mb-1 mr-5 flex font-bold pb-1">Senha</label>
              <Input
                placeholder="*********"
                :state="inputState"
                id="password"
                v-model="form.password"
                type="password"
                required
                autofocus
              />
              <p class="text-[10px]">Força da senha: <span :class="powerPassword.classes">{{ powerPassword.text }}</span></p>
            </li>
            <li class="mb-14">
              <label class="mb-1 mr-5 flex font-bold pb-1">Confirme sua senha</label>
              <Input
                placeholder="*********"
                id="confirmPassword"
                :state="isEqualInputState"
                v-model="confirmPassword"
                type="password"
                required
                autofocus
              />
              <p v-if="!isEqual" class="text-[10px] text-error">Senhas não coincidem</p>
              <p v-if="isEqual" class="text-[10px]">Força da senha: <span :class="powerPassword.classes">{{ powerPassword.text }}</span></p>
            </li>

            <li>
              <button
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
                Criar Senha
            </button>
            </li>
          </ul>
        </form>
        <div v-if="$page.props.flash.error">
          {{ $page.props.flash.error }}
        </div>

        <div v-if="$page.props.flash.success">
          {{ $page.props.flash.success }}
        </div>
        
    </div>
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
  data() {
    return {
        showModal: true,
        confirmPassword: '',
        form: this.$inertia.form({
          email: sessionStorage.getItem('recoveryEmail'),
          code: sessionStorage.getItem('code'),
          password: ''
        })
    }
  },
  methods: {
    submit() {
        if(this.allIsValid){
          this.$inertia.post('/forgot-password/new-password', this.form).then(sessionStorage.clear());
        }
    },
    isValid(fn) {
      if(fn) {
        return 'Sucesso'
      } else {
        return 'Erro'
      }
    },
  },
  computed: {
    hasEightChar() {
      return this.form.password.length > 7;
    },
    hasUpperCase() {
      var re = /([A-Z])/g
      return re.test(this.form.password);
    },
    hasLowerCase() {
      var re = /([a-z])/g
      return re.test(this.form.password);
    },
    hasNumber() {
      var re = /([0-9])/g
      return re.test(this.form.password);
    },
    isEqual() {
      return this.form.password === this.confirmPassword;
    },
    allIsValid() {
      return (this.hasEightChar && this.hasUpperCase && this.hasLowerCase && this.hasNumber)
    },
    inputState() {
      if(this.form.password) {
        if(this.allIsValid) {
          return 'success'
        } else {
          return 'error'
        }
      }
    },
    isEqualInputState() {
      if(this.form.password) {
        if(this.isEqual) {
          return 'success'
        } else {
          return 'error'
        }
      }
    },
    powerPassword() {
      if(this.allIsValid) {
        return {
          classes: 'text-success',
          text: 'forte'
        }
      }
      else if(this.hasEightChar) {
        return {
          classes: 'text-yellow-300',
          text: 'média'
        }
      } 
      else {
        return {
          classes: 'text-error',
          text: 'fraca'
        }
      }
    }
  }
}
</script>