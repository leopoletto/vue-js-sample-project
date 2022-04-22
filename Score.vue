<template>
    <Head title="Pontuação" />

    <AuthenticatedLayout>
        
        <section class="w-1/2 sm:w-full mx-auto px-5">
            <h2 class="mb-4 text-white text-center text-[28px] font-bold">Extrato</h2>

            <div class="w-full justify-center text-center">
                <Select :options="filterableMonths" v-model="form.month" :class="inputClasses" class="bg-yellow-500 text-pink-900  !text-sm w-32" placeholder="Selecione" />
            </div>

            <div class="mt-7 bg-white rounded-3xl pt-5 w-full">
                <table class="bg-white rounded-3xl w-full">
                    <thead>
                         <tr v-if="records.length === 0">
                            <th colspan="4" class="text-pink-700 font-bold text-center pt-5">
                                Não existem dados a serem exibidos
                            </th>
                        </tr>
                        <tr v-else>
                            <th class="text-xs text-pink-900 text-center pt-4 border-r border-pink-800">Data</th>
                            <th class="text-xs text-pink-900 text-center pt-4 border-r border-pink-800">Tipo</th>
                            <th class="text-xs text-pink-900 text-center pt-4 border-r border-pink-800">Descrição</th>
                            <th class="text-xs text-pink-900 text-center pt-4">Pts</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(record, index) in records" :key="index">
                            <td class="text-xs text-gray-500 text-center p-1.5 h-11 border-r border-pink-800">{{ record.created_at }}</td>
                            <td class="text-xs text-gray-500 text-center p-1.5 h-11 border-r border-pink-800">
                                <span :class="record.points > 0 ?  'text-green-600' : 'text-red-600'" class="font-bold">
                                    {{ record.points > 0 ? 'Crédito' : 'Débito' }}
                                </span>
                            </td>
                            <td class="text-xs text-gray-500 text-center p-1.5 h-11 border-r border-pink-800">{{ record.description }}</td>
                            <td class="text-xs text-gray-500 text-center p-1.5 h-11 font-bold">{{ record.points }}</td>
                        </tr>
                    </tbody>
                    <tfoot>
                        <tr>
                            <td colspan="4" class="bg-white h-14">
                                <Pagination class="mt-0" />
                            </td>
                        </tr>
                        <tr>
                            <td colspan="2" class="bg-pink-700 p-3 rounded-bl-2xl">
                                <span class="text-white font-bold">Saldo total:</span> <br>
                                <span class="text-yellow-500 text-3xl font-bold after:content-[attr(suffix)] after:text-lg" suffix="pts.">
                                    {{ balance }}
                                </span>
                            </td>
                            <td colspan="2" class="bg-pink-700 p-3 rounded-br-2xl text-right">
                                <Link class="bg-yellow-500 text-pink-900 text-[10px] font-bold p-3 leading-tight w-[86px] rounded-3xl inline-flex text-center">Clique aqui <br> e resgate</Link>
                            </td>
                        </tr>
                    </tfoot>
                </table>
            </div>
        </section>
        

    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from '@/Layouts/Authenticated.vue'
import Select from '@/Components/Select.vue';
import Pagination from '@/Components/Pagination.vue';
import { Head, Link } from '@inertiajs/inertia-vue3';

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Link,
        Select,
        Pagination
    },
    props:{
        filterableMonths: {
            type: Object,
            default: {}
        },
        records: {
            type: Array,
            default: []
        }
    },
    computed: {
        balance(){
            let balance = 0
            this.records.forEach((record) => balance += record.points)

            return balance
        }
    },
    data(){
        return {
            form: {
                month: ''
            },
            inputClasses: 'text-xs disabled:opacity-60 text-pink-900 bg-white rounded-3xl border-none px-3 py-2 leading-relaxed outline-none w-full',
        }
    }
}
</script>
