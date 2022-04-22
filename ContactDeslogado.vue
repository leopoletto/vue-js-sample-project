<template>
    <Head title="Fale Conosco" />
    <HeaderComponent :showExtras="false" />
    <Heading title="Fale Conosco" />
    <form class="px-2.5 pt-[22px]">
      <p class="text-[16px] pb-[18px]">Dúvidas ou sugestões? Fale conosco!</p>
      <InputLabelContactForm class="mb-6" labelText="Nome" :require=true inputName="nome" placeholderInput="João da Silva" />
      <InputLabelContactForm class="mb-6" labelText="Email" :require=true inputName="email" placeholderInput="joao@email.com" />
      <InputLabelContactForm class="mb-6" labelText="Telefone" :require=false inputName="telefone" placeholderInput="(00) 00000-0000" />

      <LabelContactForm for="assunto" text="Assunto" :require=true />
      <Select :modelValue="modelValue" :placeholder="placeholder" :options="options" class="mb-6 !w-full border-2"/>

      <LabelContactForm for="descricao" text="Descrição" :require=true />

      <TextArea v-model="text" v-on:input="text = $event.target.value" maxlength="800" class="h-[261px]" />
      <div class="flex justify-end">
        <span class="text-[12px] text-gray-600">{{ charactersRemaining }}/800 caracteres</span>
      </div>

      <ButtonContactForm @click.prevent="showModal = true"> 
        <span class="text-[20px] font-bold text-primary">Enviar</span> 
      </ButtonContactForm>

      <p class="mb-6"><span class="text-red-700">*</span> Campo obrigatórios.</p>
      <p class="mb-6">Informar o número de telefone é opcional, mas se informado, poderemos customizar o atendimento para você.</p>
      <p class="mb-14">A proteção de dados é a nossa prioridade. Para obter mais informações sobre como trataremos seus dados, <a class="underline text-[#2E59FF]" href="#">clique aqui</a> para acessar nossa Política de Privacidade.</p>
    </form>
    <transition>
      <div v-if="showModal" class="fixed right-0 left-0 top-0 bottom-0 z-[99] bg-[#707070] flex justify-center items-center">
        <div class="bg-white border-[1px] border-primary rounded-[4px] mx-2.5 w-full pl-4 pr-2 pt-2 pb-2 leading-9">
          <button class="float-right" @click="showModal = false">
            <Icon name="Fechar"/>
          </button>
          <h1 class="text-[20px] font-bold text-primary">Sucesso</h1>
          <p class="text-[16px]">Mensagem enviada com sucesso.</p>
        </div>
      </div>
    </transition>
    <FooterComponent />
</template>

<script>
import { Head } from '@inertiajs/inertia-vue3';
import Heading from '@/Components/UI/Texts/Heading.vue';
import HeaderComponent from "@/Components/Header.vue";
import FooterComponent from "@/Components/Footer.vue";
import LabelContactForm from "@/Components/LabelContactForm.vue";
import InputLabelContactForm from "@/Components/InputLabelContactForm.vue";
import Select from "@/Components/UI/Form/Select.vue";
import TextArea from "@/Components/TextAreaContact.vue"
import ButtonContactForm from '@/Components/ButtonContactForm.vue';
import Icon from '@/Components/UI/Icons/Icon.vue'

export default {
  components: {
    Head,
    Heading,
    HeaderComponent,
    FooterComponent,
    LabelContactForm,
    InputLabelContactForm,
    Select,
    TextArea,
    ButtonContactForm,
    Icon
  },
  data() {
    return {
      modelValue: "Assunto",
      placeholder: "Selecione um assunto",
      options: {
        assunto1: "assunto1",
        assunto2: "assunto2",
        assunto3: "assunto3",
      },
      text: '',
      showModal: false
    }
  },
  computed: {
    charactersRemaining: function () {
      return this.text.length;
    }
  }
}
</script>