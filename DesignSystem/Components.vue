<template>
    <Head title="Design System" />

    <section>
        <Group v-for="(title, group) in groups" :key="group" :title="title">
            <component :is="group" />
        </Group>
    </section>
</template>

<script>
import DesignSystem from '@/Layouts/DesignSystem.vue'
import Group from '@/Components/DesignSystem/Group.vue'
import Buttons from '@/Components/DesignSystem/Buttons.vue'
import Typography from '@/Components/DesignSystem/Typography.vue'
import Form from '@/Components/DesignSystem/Form.vue'
import Spacing from '@/Components/DesignSystem/Spacing.vue'
import Colors from '@/Components/DesignSystem/Colors.vue'
import Icons from '@/Components/DesignSystem/Icons.vue'
import Modals from '@/Components/DesignSystem/Modals.vue'
import Links from '@/Components/DesignSystem/Links.vue'
import { Head, Link } from '@inertiajs/inertia-vue3';

export default {
    layout: DesignSystem,

    components: {
        Head,
        Link,
        Modals,
        Links,
        Group,
        Buttons,
        Typography,
        Icons,
        Form,
        Spacing,
        Colors,
    },

    props: {

    },

    data() {
        return {
            groups: {
                spacing: 'Medidas de Elementos & Espaçamento',
                typography: 'Fontes',
                colors: 'Cores',
                icons: 'Ícones',
                buttons: 'Buttons',
                form: 'Form',
                modals: 'Modals',
                links: 'Links',
            }
        }
    },

    methods: {

    }
}
</script>
