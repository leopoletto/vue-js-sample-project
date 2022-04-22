<template>
    <Header :showExtras="false" />
    <Footer />
</template>
<script>
import Footer from '@/Components/Footer.vue'
import Header from '@/Components/UI/Nav/Header.vue'

export default {
    components: {
        Footer,
        Header
    }
}
</script>