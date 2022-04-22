<template>
    <Head title="Senha" />
  
    <section class="grid min-h-screen sm:pb-12 xl:grid-cols-0">
      <div class="component-background sm:hidden"></div>

      <article class="grid">
        <Header-component />
        <div class="component-background sm:hidden"></div>

      <div class="sm:px-5 xl:px-28">
        <h2 class="text-3xl font-semibold text-primary text-left xl:py-6 sm:py-4">Senha</h2>
        <p class="text-md pb-4">Crie uma <strong>senha</strong> forte que só você saiba. Ela precisa ter:</p>
        
        <ul>
          <li class="flex items-center pb-1">
            <Icon :name="isValid(hasEightChar)"/>
            <p class="ml-2.5 text-sm">Mínimo de 8 caracteres</p>
          </li>
          <li class="flex items-center pb-1">
            <Icon :name="isValid(hasUpperCase)" />
            <p class="ml-2.5 text-sm">Um caractere maiúsculo</p>
          </li>
          <li class="flex items-center pb-1">
            <Icon :name="isValid(hasLowerCase)" />
            <p nome="isValid" class="ml-2.5 text-sm">Um caractere minúsculo</p>
          </li>
          <li class="flex items-center">
            <Icon :name="isValid(hasNumber)" />
            <p class="ml-2.5 text-sm">Um número</p>
          </li>
        </ul>
        

        <form @submit.prevent="submit" class="mb-6">
          <ul class="pt-6">
            <li class="mb-4">
              <label class="mr-5 flex font-bold pb-1">Senha</label>
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
            <li class="mb-8">
              <label class="mr-5 flex font-bold pb-1">Confirme sua senha</label>
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
                    p-2
                    border-[1px]
                    rounded-sm
                    border-primary
                    hover:bg-gray-500
                    hover:border-0
                    xl:mt-0
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
          </ul>
        </form>
        <div v-if="$page.props.flash.error">
          {{ $page.props.flash.error }}
        </div>

        <div v-if="$page.props.flash.success">
          {{ $page.props.flash.success }}
        </div>
        
    </div>
    
    </article>
    </section>
    
    
</template>
<script>
import Input from '@/Components/UI/Form/Input.vue';
import Icon from '@/Components/UI/Icons/Icon.vue'
import HeaderComponent from '@/Components/Header.vue'
import Header from '@/Components/UI/Nav/Header.vue'
import Back from '@/Components/UI/Back.vue'
import { Head, Link } from "@inertiajs/inertia-vue3";

export default {
  components: {
    Header,
    Head,
    Input,
    Icon,
    Link,
    Back,
    HeaderComponent

  },
  data() {
    return {
        showModal: true,
        confirmPassword: '',
        form: this.$inertia.form({
          password: ''
        })
    }
  },
  methods: {
    submit() {
        if(this.allIsValid){
            sessionStorage.setItem('senha', this.senha);
            location.href = "/register/idade";
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