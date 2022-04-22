<template>
    <Head title="FAQ" />
    <HeaderComponent :showExtras="false" />
    <Heading title="Perguntas Frequentes" class="mb-[35px]"/>
    <div class="px-2.5 pb-[35px]">
        <Topic v-for="(topic,key) in topics" :key="key" :title="topic.title" :accordions="topic.accordions" />
    </div>
    <FooterComponent />
</template>

<script>
import { Head } from '@inertiajs/inertia-vue3';
import Heading from '@/Components/UI/Texts/Heading.vue'
import HeaderComponent from "@/Components/Header.vue";
import FooterComponent from "@/Components/Footer.vue"
import GuestLayout from "@/Layouts/Guest.vue"
import Topic from "@/Components/Topic.vue"
import Accordion from "@/Components/UI/Modals/Accordion.vue"

export default {
  layout: GuestLayout,
  components: {
    HeaderComponent,
    FooterComponent,
    Heading,
    Head,
    Accordion,
    Topic
  },
  data() {
      return {
            topics: [
                {
                title : "Tópico",
                accordions: [
                    {
                        title: "Pergunta de uma linha",
                        description: "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. "
                    },
                    {
                        title: "Pergunta de uma linha",
                        description: "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. "
                    },
                    {
                        title: "Pergunta de uma linha",
                        description: "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. "
                    }
                ]
                },
                {
                title : "Tópico",
                accordions: [
                    {
                        title: "Pergunta de uma linha",
                        description: "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. "
                    },
                    {
                        title: "Pergunta de uma linha",
                        description: "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. "
                    },
                    {
                        title: "Pergunta de uma linha",
                        description: "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. "
                    }
                ]
                },

            ]
      }
  }
  
}
</script>