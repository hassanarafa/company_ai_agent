<template>
    <div class="space-y-6">
        <h2 class="text-2xl font-bold tracking-tight text-white">Demand Intelligence</h2>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <div class="lg:col-span-2 bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl relative">
                <div class="absolute -top-3 right-6 z-10">
                    <span
                        class="px-2.5 py-0.5 text-[9px] font-extrabold uppercase tracking-wider text-black rounded-full shadow-md"
                        style="background-color: #38872c;">
                        ✨ NLP Input Module
                    </span>
                </div>
                <div>
                    <h3 class="font-bold text-sm text-white mb-1">Buyer demand</h3>
                    <p class="text-[11px] text-zinc-400">Enter a procurement requirement in natural language.</p>
                </div>

                <textarea v-model="demandText" rows="4"
                    class="w-full bg-black border border-zinc-800 rounded-xl p-4 text-xs text-white focus:outline-none transition resize-none">
        </textarea>

                <button @click="analyseDemand"
                    class="text-black font-bold px-6 py-2.5 rounded-xl text-xs transition shadow-md"
                    style="background-color: #38872c;">
                    Analyse Demand
                </button>
            </div>

            <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl">
                <div>
                    <h3 class="font-bold text-sm text-white mb-1">AI requirement extraction</h3>
                    <p class="text-[11px] text-zinc-400">AI structures the request automatically.</p>
                </div>
                <div class="bg-black border border-zinc-800 p-4 rounded-xl space-y-2 text-xs">
                    <span class="text-[9px] font-bold tracking-widest uppercase" style="color: #38872c;">STRUCTURED
                        DEMAND</span>
                    <p><span class="text-zinc-500">Category:</span> Industrial X</p>
                    <p><span class="text-zinc-500">Quantity:</span> 650,000 units</p>
                    <p><span class="text-zinc-500">Delivery window:</span> &le; 45 days</p>
                </div>
            </div>
        </div>

        <div class="bg-zinc-950 border border-zinc-900 p-6 rounded-2xl space-y-4 shadow-xl">
            <h3 class="font-bold text-sm text-white mb-1">Demand aggregation</h3>
            <div class="overflow-x-auto">
                <table class="w-full text-left text-xs">
                    <thead>
                        <tr class="border-b border-zinc-800 text-zinc-500 uppercase text-[10px]">
                            <th class="pb-3 font-semibold">BUYER</th>
                            <th class="pb-3 font-semibold">CATEGORY</th>
                            <th class="pb-3 font-semibold">DEMAND</th>
                            <th class="pb-3 font-semibold">DELIVERY</th>
                        </tr>
                    </thead>
                    <tbody class="divide-y divide-zinc-900 text-zinc-300">
                        <tr v-for="row in aggregatedDemands" :key="row.buyer" class="hover:bg-zinc-900/40 transition">
                            <td class="py-3 font-medium text-white">{{ row.buyer }}</td>
                            <td class="py-3">{{ row.category }}</td>
                            <td class="py-3 font-bold" style="color: #38872c;">{{ row.demand }}</td>
                            <td class="py-3">{{ row.delivery }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
const demandText = ref('We need 650,000 units of Industrial X delivered within 45 days.')
const aggregatedDemands = ref([
    { buyer: 'Portfolio Co. A', category: 'Industrial X', demand: '500K', delivery: '30 days' },
    { buyer: 'Portfolio Co. B', category: 'Industrial X', demand: '700K', delivery: '45 days' },
])

const analyseDemand = () => {
    aggregatedDemands.value.unshift({ buyer: 'New Portfolio', category: 'Industrial X', demand: '650K', delivery: '45 days' })
    alert('Demand successfully analyzed!')
}
</script>