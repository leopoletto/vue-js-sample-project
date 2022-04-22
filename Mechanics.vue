<template>
    <Head title="Mecânica" />

    <AuthenticatedLayout>

        <section class="sm:w-full w-1/2 mx-auto pb-10">
            <div v-for="(roleMechanics, role) in roles" :key="role" class="bg-white rounded-3xl mx-5 p-0.5 mb-6">
                <h2><a @click.prevent="currentRole = role" class="cursor-pointer w-full rounded-full bg-yellow-500 text-pink-800 text-center block py-4 text-sm font-bold">{{ role }}</a></h2>

                <div class="p-5" :class="{ 'hidden' : role !== currentRole }">
                    <h3 class="h-[76px] w-[224px] mx-auto mb-4 bg-peace-sign block bg-cover">Bateu, ganhou!</h3>

                    <p v-if="roleMechanics.starting_text" class="text-center text-xs mb-4 leading-relaxed">{{ roleMechanics.starting_text }}</p>

                    <h4 class="text-center uppercase text-xs font-bold">Gatilho</h4>
                    <p class="text-center text-xs mb-4 leading-relaxed">{{ roleMechanics.trigger }}</p>

                    <div>
                        <div v-for="(step, index) in roleMechanics.steps" :key="index" class="mb-4 relative border border-pink-800 rounded-full py-[5px] pl-9 pr-4 text-xs leading-relaxed h-[78px] flex items-center">
                            <span class="bg-pink-900 text-white rounded-full absolute top-4 -left-4 h-11 w-11 flex items-center justify-center text-lg">{{ index + 1 }}</span>
                            <p v-html="toStrong(step)"></p>
                        </div>
                    </div>

                    <template v-for="(goals, name) in roleMechanics.goals" :key="name">
                        <h4 class="w-full uppercase rounded-full bg-yellow-500 text-pink-800 items-center text-center mb-10 flex flex-col pt-2.5 text-[13px] font-bold">
                            <span class="mb-1">
                                Meta {{ name }} <br>igual ou superior a 100% 
                            </span>
                            <span class="inline-block bg-pink-800 text-yellow-500 text-[28px] -mb-5 h-11 relative rounded-full w-[105px] leading-10 font-bold after:content-[attr(suffix)] after:text-xs after:font-normal after:normal-case" suffix="pts.">
                                {{ Object.values(goals).reduce((a,b) => a + b) }}
                            </span>
                        </h4>

                        <div class="flex justify-between mb-9">
                            <div v-for="(value, name) in goals" :key="name" class="flex text-center justify-center flex-col w-[82px] h-[82px] border-[10px] border-pink-800 bg-white rounded-full">
                                <span class="font-bold text-lg leading-none text-pink-800 after:content-[attr(suffix)] after:text-xs after:font-normal" suffix="pts.">{{ value }}</span>
                                <span class="text-[9px] font-bold text-gray-500">{{ name }}</span>
                            </div>
                        </div>
                    </template>

                     <h4 class="w-full uppercase rounded-full text-yellow-500 bg-pink-800 items-center text-center mb-10 flex flex-col pt-2.5 text-xl font-bold">
                        <span class="mb-1">
                            Total
                        </span>
                        <span class="inline-block text-pink-800 bg-yellow-500 text-[28px] -mb-5 h-11 relative rounded-full w-[105px] leading-10 font-bold after:content-[attr(suffix)] after:text-xs after:font-normal after:normal-case" suffix="pts.">
                            {{ 
                                Object.values(roleMechanics.goals).reduce((a, b) => {
                                    return Object.values(a).reduce((c,d) => c + d) + Object.values(b).reduce((c,d) => c + d)
                                }) 
                            }}
                        </span>
                    </h4>

                    <p v-if="roleMechanics.finishing_text" v-html="toStrong(roleMechanics.finishing_text)" class="mb-4 relative border border-pink-800 rounded-full py-2.5 px-4 text-xs text-center leading-relaxed"></p>
                </div>
            </div>

        </section>
                
    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from '@/Layouts/Authenticated.vue'
import { Head, Link } from '@inertiajs/inertia-vue3'

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Link,
    },
    props: {
        roles: Object
    },
    data() {
        return {
            currentRole: 'Vendedor'
        }
    },
    methods: {
        toStrong(text){
            return text.replace('[', '<strong>').replace(']', '</strong>');
        }
    }
}
</script>
